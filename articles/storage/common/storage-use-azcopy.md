---
title: Copiare o spostare dati in Archiviazione di Microsoft Azure con AzCopy in Windows | Microsoft Docs
description: "Usare l'utilità AzCopy in Windows per spostare o copiare dati da o verso BLOB, tabelle e contenuto di file. Copiare i dati in archiviazione di Azure da file locali o copiare i dati all'interno o tra account di archiviazione. Migrare facilmente i dati in archiviazione di Azure."
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
ms.date: 05/14/2017
ms.author: seguler
ms.openlocfilehash: 9806697747b2409d4bd0ae19dc0b9fe01f500dc0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-data-with-the-azcopy-on-windows"></a><span data-ttu-id="78594-105">Trasferire dati con AzCopy in Windows</span><span class="sxs-lookup"><span data-stu-id="78594-105">Transfer data with the AzCopy on Windows</span></span>
<span data-ttu-id="78594-106">AzCopy è un'utilità della riga di comando progettata la copia dei dati in e da servizi di archiviazione file, tabelle e BLOB di Microsoft Azure usando semplici comandi con prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="78594-106">AzCopy is a command-line utility designed for copying data to and from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="78594-107">È possibile copiare dati da un oggetto a un altro all'interno dell'account di archiviazione o tra account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="78594-107">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="78594-108">Esistono due versioni di AzCopy che è possibile scaricare.</span><span class="sxs-lookup"><span data-stu-id="78594-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="78594-109">AzCopy in Windows viene compilato con .NET Framework e offre opzioni della riga di comando in stile Windows.</span><span class="sxs-lookup"><span data-stu-id="78594-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="78594-110">[AzCopy in Linux](storage-use-azcopy-linux.md) viene compilato con .NET Framework per le piattaforme Linux e offre opzioni della riga di comando in stile POSIX.</span><span class="sxs-lookup"><span data-stu-id="78594-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="78594-111">Questo articolo descrive AzCopy in Windows.</span><span class="sxs-lookup"><span data-stu-id="78594-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="78594-112">Scaricare e installare AzCopy</span><span class="sxs-lookup"><span data-stu-id="78594-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="78594-113">AzCopy in Windows</span><span class="sxs-lookup"><span data-stu-id="78594-113">AzCopy on Windows</span></span>
<span data-ttu-id="78594-114">Scaricare la [versione più recente di AzCopy in Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="78594-114">Download the [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="78594-115">Installazione in Windows</span><span class="sxs-lookup"><span data-stu-id="78594-115">Installation on Windows</span></span>
<span data-ttu-id="78594-116">Dopo l'installazione di AzCopy in Windows mediante il programma di installazione, aprire una finestra di comando e passare alla directory di installazione di AzCopy contenente il file eseguibile `AzCopy.exe`.</span><span class="sxs-lookup"><span data-stu-id="78594-116">After installing AzCopy on Windows using the installer, open a command window and navigate to the AzCopy installation directory on your computer - where the `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="78594-117">Se si vuole, è possibile aggiungere il percorso di installazione di AzCopy al percorso di sistema.</span><span class="sxs-lookup"><span data-stu-id="78594-117">If desired, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="78594-118">Per impostazione predefinita, AzCopy viene installato in `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` o `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="78594-118">By default, AzCopy is installed to `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="78594-119">Scrittura del primo comando AzCopy </span><span class="sxs-lookup"><span data-stu-id="78594-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="78594-120">La sintassi di base per i comandi di AzCopy è la seguente:</span><span class="sxs-lookup"><span data-stu-id="78594-120">The basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="78594-121">Gli esempi seguenti illustrano vari scenari per la copia dei dati da e in e da BLOB, file e tabelle di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="78594-121">The following examples demonstrate a variety of scenarios for copying data to and from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="78594-122">Per una spiegazione dettagliata dei parametri usati in ogni esempio, vedere la sezione [Parametri di AzCopy](#azcopy-parameters) .</span><span class="sxs-lookup"><span data-stu-id="78594-122">Refer to the [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="78594-123">BLOB: scaricare</span><span class="sxs-lookup"><span data-stu-id="78594-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="78594-124">Scaricare un singolo BLOB</span><span class="sxs-lookup"><span data-stu-id="78594-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="78594-125">Se la cartella `C:\myfolder` non esiste ancora, AzCopy la crea e scarica `abc.txt ` nella nuova cartella.</span><span class="sxs-lookup"><span data-stu-id="78594-125">Note that if the folder `C:\myfolder` does not exist, AzCopy creates it and download `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="78594-126">Scaricare un singolo BLOB da un'area secondaria</span><span class="sxs-lookup"><span data-stu-id="78594-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="78594-127">È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="78594-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="78594-128">Scaricare tutti BLOB</span><span class="sxs-lookup"><span data-stu-id="78594-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="78594-129">Si supponga che i BLOB seguenti risiedano nel contenitore specificato:</span><span class="sxs-lookup"><span data-stu-id="78594-129">Assume the following blobs reside in the specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="78594-130">Dopo l'operazione di download, la directory `C:\myfolder` include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="78594-130">After the download operation, the directory `C:\myfolder` includes the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="78594-131">Se non si specifica l'opzione `/S`, non verrà scaricato alcun BLOB.</span><span class="sxs-lookup"><span data-stu-id="78594-131">If you do not specify option `/S`, no blobs are downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="78594-132">Scaricare i BLOB con il prefisso specificato</span><span class="sxs-lookup"><span data-stu-id="78594-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="78594-133">Si supponga che i BLOB seguenti risiedano nel contenitore specificato.</span><span class="sxs-lookup"><span data-stu-id="78594-133">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="78594-134">Vengono scaricati tutti i BLOB che iniziano con il prefisso `a`:</span><span class="sxs-lookup"><span data-stu-id="78594-134">All blobs beginning with the prefix `a` are downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="78594-135">Dopo l'operazione di download, la cartella `C:\myfolder` include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="78594-135">After the download operation, the folder `C:\myfolder` includes the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="78594-136">Il prefisso si applica alla directory virtuale che forma la prima parte del nome del BLOB.</span><span class="sxs-lookup"><span data-stu-id="78594-136">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="78594-137">Nell'esempio precedente, la directory virtuale non corrisponde al prefisso specificato, quindi non viene scaricata.</span><span class="sxs-lookup"><span data-stu-id="78594-137">In the example shown above, the virtual directory does not match the specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="78594-138">Se inoltre l'opzione `\S` non è specificata, AzCopy non scarica alcun BLOB.</span><span class="sxs-lookup"><span data-stu-id="78594-138">In addition, if the option `\S` is not specified, AzCopy does not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="78594-139">Impostare l'ora dell'ultima modifica dei file esportati sulla stessa ora dei BLOB di origine</span><span class="sxs-lookup"><span data-stu-id="78594-139">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="78594-140">È anche possibile escludere BLOB dall'operazione di download in base all'ora dell'ultima modifica.</span><span class="sxs-lookup"><span data-stu-id="78594-140">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="78594-141">Se ad esempio si vogliono escludere i BLOB in cui l'ora dell'ultima modifica è uguale o successiva a quella del file di destinazione, aggiungere l'opzione `/XN` .</span><span class="sxs-lookup"><span data-stu-id="78594-141">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="78594-142">In alternativa, se si vogliono escludere i BLOB in cui l'ora dell'ultima modifica è uguale o precedente a quella del file di destinazione, aggiungere l'opzione `/XO` .</span><span class="sxs-lookup"><span data-stu-id="78594-142">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="78594-143">BLOB: caricare</span><span class="sxs-lookup"><span data-stu-id="78594-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="78594-144">Caricare un singolo file</span><span class="sxs-lookup"><span data-stu-id="78594-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="78594-145">Se il contenitore di destinazione specificato non esiste, AzCopy ne crea uno e vi carica il file.</span><span class="sxs-lookup"><span data-stu-id="78594-145">If the specified destination container does not exist, AzCopy creates it and uploads the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="78594-146">Caricare un singolo file nella directory virtuale</span><span class="sxs-lookup"><span data-stu-id="78594-146">Upload single file to virtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="78594-147">Se la directory virtuale specificata non esiste, AzCopy carica il file in modo da includere la directory virtuale nel nome del BLOB, *ovvero* `vd/abc.txt` nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="78594-147">If the specified virtual directory does not exist, AzCopy uploads the file to include the virtual directory in its name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="78594-148">Caricare tutti i file</span><span class="sxs-lookup"><span data-stu-id="78594-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="78594-149">Se si specifica l'opzione `/S`, il contenuto della directory specificata viene caricato nell'archiviazione BLOB in modo ricorsivo, ovvero vengono caricati anche tutte le sottocartelle e i relativi file.</span><span class="sxs-lookup"><span data-stu-id="78594-149">Specifying option `/S` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files are uploaded as well.</span></span> <span data-ttu-id="78594-150">Si supponga ad esempio che i file seguenti risiedano nella cartella `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="78594-150">For instance, assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="78594-151">Dopo l'operazione di caricamento, il contenitore include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="78594-151">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="78594-152">Se non si specifica l'opzione `/S`, AzCopy non carica i file in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="78594-152">If you do not specify option `/S`, AzCopy does not upload recursively.</span></span> <span data-ttu-id="78594-153">Dopo l'operazione di caricamento, il contenitore include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="78594-153">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="78594-154">Caricare i file corrispondenti ai criteri specificati</span><span class="sxs-lookup"><span data-stu-id="78594-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="78594-155">Si supponga che i file seguenti risiedano nella cartella `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="78594-155">Assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="78594-156">Dopo l'operazione di caricamento, il contenitore include i file seguenti:</span><span class="sxs-lookup"><span data-stu-id="78594-156">After the upload operation, the container includes the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="78594-157">Se non si specifica l'opzione `/S`, AzCopy carica solo i BLOB che non si trovano in una directory virtuale:</span><span class="sxs-lookup"><span data-stu-id="78594-157">If you do not specify option `/S`, AzCopy only uploads blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="78594-158">Specificare il tipo di contenuto MIME di un BLOB di destinazione</span><span class="sxs-lookup"><span data-stu-id="78594-158">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="78594-159">Per impostazione predefinita, AzCopy imposta il tipo di contenuto di un BLOB di destinazione su `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="78594-159">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="78594-160">A partire dalla versione 3.1.0, è possibile specificare il tipo di contenuto in modo esplicito tramite l'opzione `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="78594-160">Beginning with version 3.1.0, you can explicitly specify the content type via the option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="78594-161">Questa sintassi imposta il tipo di contenuto per tutti i BLOB in un'operazione di caricamento.</span><span class="sxs-lookup"><span data-stu-id="78594-161">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="78594-162">Se si specifica `/SetContentType` senza fornire un valore, AzCopy imposta il tipo di contenuto di ogni BLOB o file in base alla loro estensione.</span><span class="sxs-lookup"><span data-stu-id="78594-162">If you specify `/SetContentType` without a value, AzCopy sets each blob or file's content type according to its file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="78594-163">BLOB: copiare</span><span class="sxs-lookup"><span data-stu-id="78594-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="78594-164">Copiare un BLOB all'interno di un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="78594-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="78594-165">Quando si copia un BLOB all'interno di un account di archiviazione, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="78594-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="78594-166">Copiare un singolo BLOB tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="78594-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="78594-167">Quando si copia un BLOB tra account di archiviazione, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="78594-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="78594-168">Copiare in BLOB singolo da un'area secondaria all'area primaria</span><span class="sxs-lookup"><span data-stu-id="78594-168">Copy single blob from secondary region to primary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="78594-169">È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="78594-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="78594-170">Copiare un singolo BLOB e i relativi snapshot tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="78594-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="78594-171">Dopo l'operazione di copia, il contenitore di destinazione include il BLOB e i relativi snapshot.</span><span class="sxs-lookup"><span data-stu-id="78594-171">After the copy operation, the target container includes the blob and its snapshots.</span></span> <span data-ttu-id="78594-172">Supponendo che il BLOB dell'esempio precedente contenga due snapshot, nel contenitore saranno presenti il BLOB e gli snapshot seguenti:</span><span class="sxs-lookup"><span data-stu-id="78594-172">Assuming the blob in the example above has two snapshots, the container includes the following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="78594-173">Copiare in modo sincrono i BLOB tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="78594-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="78594-174">Per impostazione predefinita, AzCopy copia i dati tra due endpoint di archiviazione in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="78594-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="78594-175">L'operazione di copia viene quindi eseguita in background sfruttando la capacità di larghezza di banda disponibile non limitata da alcun contratto di servizio relativo alla velocità di copia di un BLOB. AzCopy, inoltre, controlla periodicamente lo stato della copia fino a quando questa non viene completata o risulta non riuscita.</span><span class="sxs-lookup"><span data-stu-id="78594-175">Therefore, the copy operation runs in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob is copied, and AzCopy periodically checks the copy status until the copying is completed or failed.</span></span>

<span data-ttu-id="78594-176">L'opzione `/SyncCopy` garantisce che l'operazione di copia avvenga a velocità costante.</span><span class="sxs-lookup"><span data-stu-id="78594-176">The `/SyncCopy` option ensures that the copy operation gets consistent speed.</span></span> <span data-ttu-id="78594-177">AzCopy esegue la copia sincrona scaricando i BLOB da copiare dall'origine specificata nella memoria locale, per poi caricarli nella destinazione dell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="78594-177">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="78594-178">`/SyncCopy` potrebbe generare costi di uscita aggiuntivi rispetto alla copia asincrona. Per evitare costi di uscita, è quindi consigliabile usare questa opzione in una VM di Azure che si trova nella stessa area dell'account di archiviazione di origine.</span><span class="sxs-lookup"><span data-stu-id="78594-178">`/SyncCopy` might generate additional egress cost compared to asynchronous copy, the recommended approach is to use this option in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="78594-179">File: scaricare</span><span class="sxs-lookup"><span data-stu-id="78594-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="78594-180">Scaricare un singolo file</span><span class="sxs-lookup"><span data-stu-id="78594-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="78594-181">Se l'origine specificata è una condivisione file di Azure, è necessario specificare il nome file esatto, *ad esempio* `abc.txt`, per copiare un solo file oppure specificare l'opzione `/S` per copiare tutti i file nella condivisione in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="78594-181">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `/S` to download all files in the share recursively.</span></span> <span data-ttu-id="78594-182">Se si specificano sia il criterio del file che l'opzione `/S` contemporaneamente, verrà generato un errore.</span><span class="sxs-lookup"><span data-stu-id="78594-182">Attempting to specify both a file pattern and option `/S` together results in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="78594-183">Scaricare tutti i file</span><span class="sxs-lookup"><span data-stu-id="78594-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="78594-184">Le cartelle vuote non vengono scaricate.</span><span class="sxs-lookup"><span data-stu-id="78594-184">Note that any empty folders are not downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="78594-185">File: caricare</span><span class="sxs-lookup"><span data-stu-id="78594-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="78594-186">Caricare un singolo file</span><span class="sxs-lookup"><span data-stu-id="78594-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="78594-187">Caricare tutti i file</span><span class="sxs-lookup"><span data-stu-id="78594-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="78594-188">Le cartelle vuote non vengono caricate.</span><span class="sxs-lookup"><span data-stu-id="78594-188">Note that any empty folders are not uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="78594-189">Caricare i file corrispondenti ai criteri specificati</span><span class="sxs-lookup"><span data-stu-id="78594-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="78594-190">File: copia</span><span class="sxs-lookup"><span data-stu-id="78594-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="78594-191">Copiare tra condivisioni file</span><span class="sxs-lookup"><span data-stu-id="78594-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="78594-192">Quando si copia un file tra condivisioni file, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="78594-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="78594-193">Copiare dalla condivisione file al BLOB</span><span class="sxs-lookup"><span data-stu-id="78594-193">Copy from file share to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="78594-194">Quando si copia un file dalla condivisione file al BLOB, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="78594-194">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="78594-195">Copy dal BLOB alla condivisione file</span><span class="sxs-lookup"><span data-stu-id="78594-195">Copy from blob to file share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="78594-196">Quando si copia un file dal BLOB alla condivisione file, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="78594-196">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="78594-197">Copiare file in modo sincrono</span><span class="sxs-lookup"><span data-stu-id="78594-197">Synchronously copy files</span></span>
<span data-ttu-id="78594-198">È possibile specificare l'opzione `/SyncCopy` per copiare i dati da archiviazione file ad archiviazione file, da archiviazione file ad archivio BLOB e da archivio BLOB ad archiviazione file in modo sincrono. AzCopy esegue questa operazione scaricando i dati di origine nella memoria locale e caricandoli di nuovo nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="78594-198">You can specify the `/SyncCopy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously, AzCopy does this by downloading the source data to local memory and upload it again to destination.</span></span> <span data-ttu-id="78594-199">Vengono applicati i costi in uscita standard.</span><span class="sxs-lookup"><span data-stu-id="78594-199">Standard egress cost applies.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="78594-200">Durante la copia da Archiviazione file ad Archiviazione BLOB, il tipo di BLOB predefinito è il BLOB in blocchi. Per modificare il tipo di BLOB di destinazione, è possibile specificare l'opzione `/BlobType:page`.</span><span class="sxs-lookup"><span data-stu-id="78594-200">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="78594-201">Notare che `/SyncCopy` potrebbe generare ulteriori costi in uscita rispetto alla copia asincrona. Per evitare costi di uscita, è dunque consigliabile usare questa opzione nella macchina virtuale di Azure che si trova nella stessa area dell'account di archiviazione di origine.</span><span class="sxs-lookup"><span data-stu-id="78594-201">Note that `/SyncCopy` might generate additional egress cost comparing to asynchronous copy, the recommended approach is to use this option in the Azure VM which is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="78594-202">Tabella: esportare</span><span class="sxs-lookup"><span data-stu-id="78594-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="78594-203">Esportare una tabella</span><span class="sxs-lookup"><span data-stu-id="78594-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="78594-204">AzCopy scrive un file manifesto nella cartella di destinazione specificata.</span><span class="sxs-lookup"><span data-stu-id="78594-204">AzCopy writes a manifest file to the specified destination folder.</span></span> <span data-ttu-id="78594-205">Il file manifesto viene usato dal processo di importazione per trovare i file di dati necessari ed eseguire la convalida di dati.</span><span class="sxs-lookup"><span data-stu-id="78594-205">The manifest file is used in the import process to locate the necessary data files and perform data validation.</span></span> <span data-ttu-id="78594-206">Il file manifesto usa per impostazione predefinita la convenzione di denominazione seguente:</span><span class="sxs-lookup"><span data-stu-id="78594-206">The manifest file uses the following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="78594-207">È possibile anche specificare l'opzione `/Manifest:<manifest file name>` per impostare il nome del file manifesto.</span><span class="sxs-lookup"><span data-stu-id="78594-207">User can also specify the option `/Manifest:<manifest file name>` to set the manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="78594-208">Dividere l'esportazione in più file</span><span class="sxs-lookup"><span data-stu-id="78594-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="78594-209">AzCopy usa un *indice di volumi* nei nomi file di dati divisi per distinguere più file.</span><span class="sxs-lookup"><span data-stu-id="78594-209">AzCopy uses a *volume index* in the split data file names to distinguish multiple files.</span></span> <span data-ttu-id="78594-210">L'indice di volumi è costituito da due parti, un *indice di intervalli di chiavi di partizione* e un *indice di file divisi*.</span><span class="sxs-lookup"><span data-stu-id="78594-210">The volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="78594-211">Entrambi gli indici sono in base zero.</span><span class="sxs-lookup"><span data-stu-id="78594-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="78594-212">L'indice dell'intervallo di chiavi di partizione è 0 se l'utente non specifica l'opzione `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="78594-212">The partition key range index is 0 if the user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="78594-213">Si supponga, ad esempio, che AzCopy generi due file di dati dopo che l'utente ha specificato l'opzione. `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="78594-213">For instance, suppose AzCopy generates two data files after the user specifies option `/SplitSize`.</span></span> <span data-ttu-id="78594-214">I nomi file di dati risultanti potrebbero essere:</span><span class="sxs-lookup"><span data-stu-id="78594-214">The resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="78594-215">Tenere presente che il valore minimo possibile per l'opzione `/SplitSize` è di 32 MB.</span><span class="sxs-lookup"><span data-stu-id="78594-215">Note that the minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="78594-216">Se la destinazione specificata è l'archiviazione BLOB, AzCopy divide il file di dati quando le dimensioni raggiungono il limite delle dimensioni BLOB (200 GB), indipendentemente dal fatto che l'opzione `/SplitSize` sia stata specificata o meno dall'utente.</span><span class="sxs-lookup"><span data-stu-id="78594-216">If the specified destination is Blob storage, AzCopy splits the data file once its sizes reaches the blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by the user.</span></span>

### <a name="export-table-to-json-or-csv-data-file-format"></a><span data-ttu-id="78594-217">Esportare la tabella nel formato di file di dati JSON o CSV</span><span class="sxs-lookup"><span data-stu-id="78594-217">Export table to JSON or CSV data file format</span></span>
<span data-ttu-id="78594-218">Per impostazione predefinita, AzCopy esporta le tabelle in file di dati JSON.</span><span class="sxs-lookup"><span data-stu-id="78594-218">AzCopy by default exports tables to JSON data files.</span></span> <span data-ttu-id="78594-219">È possibile specificare l'opzione `/PayloadFormat:JSON|CSV` per esportare le tabelle come JSON o CSV.</span><span class="sxs-lookup"><span data-stu-id="78594-219">You can specify the option `/PayloadFormat:JSON|CSV` to export the tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="78594-220">Quando si specifica il formato di payload CSV, AzCopy genera anche un file di schema con estensione `.schema.csv` per ogni file di dati.</span><span class="sxs-lookup"><span data-stu-id="78594-220">When specifying the CSV payload format, AzCopy also generates a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="78594-221">Esportare entità tabella simultaneamente</span><span class="sxs-lookup"><span data-stu-id="78594-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="78594-222">AzCopy avvia operazioni simultanee per esportare le entità quando l'utente specifica l'opzione `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="78594-222">AzCopy starts concurrent operations to export entities when the user specifies option `/PKRS`.</span></span> <span data-ttu-id="78594-223">Ogni operazione esporta un intervallo di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="78594-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="78594-224">Si noti che il numero di operazioni simultanee viene controllato anche dall'opzione `/NC`.</span><span class="sxs-lookup"><span data-stu-id="78594-224">Note that the number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="78594-225">AzCopy usa il numero di processori core come valore predefinito di `/NC`durante la copia di entità della tabella, anche se `/NC` non è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="78594-225">AzCopy uses the number of core processors as the default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="78594-226">Quando l'utente specifica l'opzione `/PKRS`, AzCopy usa il valore più basso dei due (intervalli di chiavi di partizione e operazioni simultanee specificate in modo implicito o esplicito) per determinare il numero di operazioni simultanee da avviare.</span><span class="sxs-lookup"><span data-stu-id="78594-226">When the user specifies option `/PKRS`, AzCopy uses the smaller of the two values - partition key ranges versus implicitly or explicitly specified concurrent operations - to determine the number of concurrent operations to start.</span></span> <span data-ttu-id="78594-227">Per ulteriori dettagli, digitare `AzCopy /?:NC` nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="78594-227">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="export-table-to-blob"></a><span data-ttu-id="78594-228">Esportare una tabella in un BLOB</span><span class="sxs-lookup"><span data-stu-id="78594-228">Export table to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="78594-229">AzCopy genera un file di dati JSON nel contenitore BLOB con la convenzione di denominazione seguente:</span><span class="sxs-lookup"><span data-stu-id="78594-229">AzCopy generates a JSON data file into the blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="78594-230">Il file di dati JSON generato segue il formato di payload per i metadati minimi.</span><span class="sxs-lookup"><span data-stu-id="78594-230">The generated JSON data file follows the payload format for minimal metadata.</span></span> <span data-ttu-id="78594-231">Per i dettagli su questo formato di payload, vedere [Formato di payload per le operazioni del servizio tabelle](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="78594-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="78594-232">Quando si esportano tabelle in file BLOB, AzCopy scarica le entità tabella in file di dati temporanei locali e quindi le carica nei file BLOB.</span><span class="sxs-lookup"><span data-stu-id="78594-232">Note that when exporting tables to blobs, AzCopy downloads the Table entities to local temporary data files and then uploads those entities to the blob.</span></span> <span data-ttu-id="78594-233">Questi file di dati temporanei vengono inseriti nella cartella di file journal con il percorso predefinito "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>". È possibile specificare l'opzione /Z:[journal-file-folder] per modificare il percorso della cartella di file journal e quindi modificare il percorso dei file di dati temporanei.</span><span class="sxs-lookup"><span data-stu-id="78594-233">These temporary data files are put into the journal file folder with the default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] to change the journal file folder location and thus change the temporary data files location.</span></span> <span data-ttu-id="78594-234">Le dimensioni dei file di dati temporanei dipendono dalle dimensioni delle entità tabella e dalle dimensioni specificate con l'opzione /SplitSize, anche se il file di dati temporanei sul disco locale viene eliminato immediatamente dopo essere stato caricato nel BLOB. Verificare che lo spazio disponibile sul disco locale sia sufficiente per archiviare i file di dati temporanei prima che vengano eliminati.</span><span class="sxs-lookup"><span data-stu-id="78594-234">The temporary data files' size is decided by your table entities' size and the size you specified with the option /SplitSize, although the temporary data file in local disk is deleted instantly once it has been uploaded to the blob, please make sure you have enough local disk space to store these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="78594-235">Tabella: importare</span><span class="sxs-lookup"><span data-stu-id="78594-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="78594-236">Importare una tabella</span><span class="sxs-lookup"><span data-stu-id="78594-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="78594-237">L'opzione `/EntityOperation` indica come inserire le entità nella tabella.</span><span class="sxs-lookup"><span data-stu-id="78594-237">The option `/EntityOperation` indicates how to insert entities into the table.</span></span> <span data-ttu-id="78594-238">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="78594-238">Possible values are:</span></span>

* <span data-ttu-id="78594-239">`InsertOrSkip`: ignora un'entità esistente oppure ne inserisce una nuova se non esiste nella tabella.</span><span class="sxs-lookup"><span data-stu-id="78594-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="78594-240">`InsertOrMerge`: unisce un'entità esistente oppure ne inserisce una nuova se non esiste nella tabella.</span><span class="sxs-lookup"><span data-stu-id="78594-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="78594-241">`InsertOrReplace`: sostituisce un'entità esistente oppure ne inserisce una nuova se non esiste nella tabella.</span><span class="sxs-lookup"><span data-stu-id="78594-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="78594-242">Si noti che non è possibile specificare l'opzione `/PKRS`nello scenario di importazione.</span><span class="sxs-lookup"><span data-stu-id="78594-242">Note that you cannot specify option `/PKRS` in the import scenario.</span></span> <span data-ttu-id="78594-243">Diversamente dallo scenario di esportazione, in cui è necessario specificare l'opzione `/PKRS` per avviare operazioni simultanee, quando si importa una tabella, AzCopy avvia l'esecuzione di operazioni simultanee per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="78594-243">Unlike the export scenario, in which you must specify option `/PKRS` to start concurrent operations, AzCopy starts concurrent operations by default when you import a table.</span></span> <span data-ttu-id="78594-244">Il numero predefinito di operazioni simultanee avviate è uguale al numero di processori core. Tuttavia, è possibile specificare un numero diverso di operazioni simultanee con l'opzione`/NC`.</span><span class="sxs-lookup"><span data-stu-id="78594-244">The default number of concurrent operations started is equal to the number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="78594-245">Per ulteriori dettagli, digitare `AzCopy /?:NC` nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="78594-245">For more details, type `AzCopy /?:NC` at the command line.</span></span>

<span data-ttu-id="78594-246">Si noti che AzCopy supporta solo l'importazione per JSON, non per CSV.</span><span class="sxs-lookup"><span data-stu-id="78594-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="78594-247">AzCopy non supporta l'importazione di tabelle da file JSON e file manifesto creati dall'utente.</span><span class="sxs-lookup"><span data-stu-id="78594-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="78594-248">Entrambi questi file devono provenire da un'esportazione di tabella di AzCopy.</span><span class="sxs-lookup"><span data-stu-id="78594-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="78594-249">Per evitare errori, non modificare il file JSON o il file manifesto esportato.</span><span class="sxs-lookup"><span data-stu-id="78594-249">To avoid errors, please do not modify the exported JSON or manifest file.</span></span>

### <a name="import-entities-to-table-using-blobs"></a><span data-ttu-id="78594-250">Importare entità nella tabella usando i BLOB</span><span class="sxs-lookup"><span data-stu-id="78594-250">Import entities to table using blobs</span></span>
<span data-ttu-id="78594-251">Si supponga che in un contenitore BLOB siano presenti: un file JSON che rappresenta una tabella di Azure e il relativo file manifesto associato.</span><span class="sxs-lookup"><span data-stu-id="78594-251">Assume a Blob container contains the following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="78594-252">È possibile eseguire il comando seguente per importare le entità in una tabella usando il file manifesto disponibile nel contenitore BLOB:</span><span class="sxs-lookup"><span data-stu-id="78594-252">You can run the following command to import entities into a table using the manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="78594-253">Altre funzionalità di AzCopy</span><span class="sxs-lookup"><span data-stu-id="78594-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="78594-254">Copiare solo i dati che non esistono nella destinazione</span><span class="sxs-lookup"><span data-stu-id="78594-254">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="78594-255">I parametri `/XO` e `/XN` consentono di escludere dalla copia, rispettivamente, le risorse di origine precedenti o più recenti.</span><span class="sxs-lookup"><span data-stu-id="78594-255">The `/XO` and `/XN` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="78594-256">Per copiare solo e risorse di origine che non esistono nella destinazione, è possibile specificare entrambi i parametri nel comando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="78594-256">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="78594-257">Si noti che questi parametri non sono supportati quando l'origine o la destinazione è una tabella.</span><span class="sxs-lookup"><span data-stu-id="78594-257">Note that this is not supported when either the source or destination is a table.</span></span>

### <a name="use-a-response-file-to-specify-command-line-parameters"></a><span data-ttu-id="78594-258">Usare un file di risposta per specificare i parametri della riga di comando</span><span class="sxs-lookup"><span data-stu-id="78594-258">Use a response file to specify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="78594-259">È possibile includere i parametri della riga di comando di AzCopy in un file di risposta.</span><span class="sxs-lookup"><span data-stu-id="78594-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="78594-260">AzCopy elabora i parametri nel file come se fossero stati specificati nella riga di comando, eseguendo una sostituzione diretta con i contenuti del file.</span><span class="sxs-lookup"><span data-stu-id="78594-260">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="78594-261">Si supponga che sia presente un file di risposta denominato `copyoperation.txt`, che contiene le righe seguenti.</span><span class="sxs-lookup"><span data-stu-id="78594-261">Assume a response file named `copyoperation.txt`, that contains the following lines.</span></span> <span data-ttu-id="78594-262">Ogni parametro di AzCopy può essere specificato su una singola riga</span><span class="sxs-lookup"><span data-stu-id="78594-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="78594-263">o su righe separate:</span><span class="sxs-lookup"><span data-stu-id="78594-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="78594-264">Se il parametro viene suddiviso su due righe, l'operazione di AzCopy ha esito negativo, come mostrato di seguito per il parametro `/sourcekey`:</span><span class="sxs-lookup"><span data-stu-id="78594-264">AzCopy fails if you split the parameter across two lines, as shown here for the `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-to-specify-command-line-parameters"></a><span data-ttu-id="78594-265">Usare più file di risposta per specificare i parametri della riga di comando</span><span class="sxs-lookup"><span data-stu-id="78594-265">Use multiple response files to specify command-line parameters</span></span>
<span data-ttu-id="78594-266">Si supponga che siano presenti un file di risposta denominato `source.txt` , che specifica un contenitore di origine:</span><span class="sxs-lookup"><span data-stu-id="78594-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="78594-267">Un file di risposta denominato `dest.txt` , che specifica una cartella di destinazione nel file system:</span><span class="sxs-lookup"><span data-stu-id="78594-267">And a response file named `dest.txt` that specifies a destination folder in the file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="78594-268">E un file di risposta denominato `options.txt` , che specifica le opzioni per AzCopy:</span><span class="sxs-lookup"><span data-stu-id="78594-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="78594-269">Per chiamare AzCopy con questi file di risposta, che risiedono in una directory `C:\responsefiles`, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="78594-269">To call AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="78594-270">AzCopy elabora il comando come se fossero stati inclusi tutti i singoli parametri nella riga di comando:</span><span class="sxs-lookup"><span data-stu-id="78594-270">AzCopy processes this command just as it would if you included all of the individual parameters on the command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="78594-271">Specificare una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="78594-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="78594-272">È anche possibile specificare una firma di accesso condiviso per il contenitore URI:</span><span class="sxs-lookup"><span data-stu-id="78594-272">You can also specify a SAS on the container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="78594-273">Cartella del file journal</span><span class="sxs-lookup"><span data-stu-id="78594-273">Journal file folder</span></span>
<span data-ttu-id="78594-274">Ogni volta che si invia un comando ad AzCopy, l'utilità verifica se il file journal è presente nella cartella predefinita o in una cartella specificata dall'utente tramite questa opzione.</span><span class="sxs-lookup"><span data-stu-id="78594-274">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="78594-275">Se il file journal non viene trovato in tali percorsi, AzCopy considera l'operazione come nuova e quindi crea un nuovo file journal.</span><span class="sxs-lookup"><span data-stu-id="78594-275">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="78594-276">Se il file journal esiste, AzCopy verifica se la riga di comando di input corrisponde alla riga di comando nel file journal.</span><span class="sxs-lookup"><span data-stu-id="78594-276">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="78594-277">Se le righe di comando corrispondono, AzCopy avvia la ripresa dell'operazione incompleta.</span><span class="sxs-lookup"><span data-stu-id="78594-277">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="78594-278">Se non corrispondono, viene chiesto se si vuole sovrascrivere il file journal per avviare una nuova operazione o annullare l'operazione corrente.</span><span class="sxs-lookup"><span data-stu-id="78594-278">If they do not match, you are prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="78594-279">Se si vuole usare il percorso predefinito per il file journal:</span><span class="sxs-lookup"><span data-stu-id="78594-279">If you want to use the default location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="78594-280">Se si omette l'opzione`/Z` o si specifica l'opzione `/Z` senza il percorso della cartella, come illustrato sopra, AzCopy creerà il file journal nel percorso predefinito, ovvero `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="78594-280">If you omit option `/Z`, or specify option `/Z` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="78594-281">Se il file journal esiste già, AzCopy riprenderà l'operazione in base al file journal.</span><span class="sxs-lookup"><span data-stu-id="78594-281">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="78594-282">Se si vuole specificare un percorso personalizzato per il file journal:</span><span class="sxs-lookup"><span data-stu-id="78594-282">If you want to specify a custom location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="78594-283">In questo esempio viene creato il file journal, nel caso in cui non esista già:</span><span class="sxs-lookup"><span data-stu-id="78594-283">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="78594-284">Se esiste, AzCopy riprenderà l'operazione in base al file journal.</span><span class="sxs-lookup"><span data-stu-id="78594-284">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="78594-285">Se si vuole riprendere un'operazione di AzCopy:</span><span class="sxs-lookup"><span data-stu-id="78594-285">If you want to resume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="78594-286">In questo esempio viene ripresa l'ultima operazione che potrebbe non essere stata completata a causa di errori.</span><span class="sxs-lookup"><span data-stu-id="78594-286">This example resumes the last operation, which may have failed to complete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="78594-287">Generare un file di log</span><span class="sxs-lookup"><span data-stu-id="78594-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="78594-288">Se si specifica l'opzione `/V`senza fornire il percorso del file di log dettagliato, AzCopy creerà il file journal nel percorso predefinito, ovvero`%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="78594-288">If you specify option `/V` without providing a file path to the verbose log, then AzCopy creates the log file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="78594-289">In caso contrario, è possibile creare un file di log in un percorso personalizzato:</span><span class="sxs-lookup"><span data-stu-id="78594-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="78594-290">Si noti che se si specifica un percorso relativo per l'opzione`/V` , ad esempio`/V:test/azcopy1.log`, il log dettagliato verrà creato nella directory di lavoro corrente all'interno di una sottocartella denominata `test`.</span><span class="sxs-lookup"><span data-stu-id="78594-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then the verbose log is created in the current working directory within a subfolder named `test`.</span></span>

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="78594-291">Specificare il numero di operazioni simultanee da avviare</span><span class="sxs-lookup"><span data-stu-id="78594-291">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="78594-292">L'opzione `/NC` specifica il numero di operazioni di copia simultanee.</span><span class="sxs-lookup"><span data-stu-id="78594-292">Option `/NC` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="78594-293">Per impostazione predefinita, AzCopy avvia un determinato numero di operazioni simultanee per aumentare la velocità effettiva di trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="78594-293">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="78594-294">Per le operazioni su tabella il numero di operazioni simultanee è uguale al numero di processori disponibili.</span><span class="sxs-lookup"><span data-stu-id="78594-294">For Table operations, the number of concurrent operations is equal to the number of processors you have.</span></span> <span data-ttu-id="78594-295">Per le operazioni su BLOB e file il numero di operazioni simultanee è pari a 8 volte il numero di processori disponibili.</span><span class="sxs-lookup"><span data-stu-id="78594-295">For Blob and File operations, the number of concurrent operations is equal 8 times the number of processors you have.</span></span> <span data-ttu-id="78594-296">Se AzCopy è in esecuzione in una rete con larghezza di banda ridotta, è possibile specificare un numero inferiore per il parametro /NC in modo da evitare errori generati dalla competizione tra le risorse.</span><span class="sxs-lookup"><span data-stu-id="78594-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC to avoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="78594-297">Eseguire AzCopy nell'Emulatore di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="78594-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="78594-298">È possibile eseguire AzCopy nell' [Emulatore di archiviazione di Azure](storage-use-emulator.md) per i BLOB:</span><span class="sxs-lookup"><span data-stu-id="78594-298">You can run AzCopy against the [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="78594-299">e le tabelle:</span><span class="sxs-lookup"><span data-stu-id="78594-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="78594-300">Parametri di AzCopy</span><span class="sxs-lookup"><span data-stu-id="78594-300">AzCopy Parameters</span></span>
<span data-ttu-id="78594-301">I parametri per AzCopy sono descritti nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="78594-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="78594-302">È anche possibile digitare uno dei comandi seguenti dalla riga di comando per assistenza nell'uso di AzCopy:</span><span class="sxs-lookup"><span data-stu-id="78594-302">You can also type one of the following commands from the command line for help in using AzCopy:</span></span>

* <span data-ttu-id="78594-303">Per assistenza dettagliata della riga di comando per AzCopy: `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="78594-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="78594-304">Per assistenza dettagliata con un parametro di AzCopy: `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="78594-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="78594-305">Per esempi della riga di comando: `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="78594-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="78594-306">/Source: "source"</span><span class="sxs-lookup"><span data-stu-id="78594-306">/Source:"source"</span></span>
<span data-ttu-id="78594-307">Specifica i dati di origine da cui eseguire la copia.</span><span class="sxs-lookup"><span data-stu-id="78594-307">Specifies the source data from which to copy.</span></span> <span data-ttu-id="78594-308">L'origine può essere una directory di file system, un contenitore BLOB, una directory virtuale BLOB, una condivisione file di archiviazione, una directory file di archiviazione o una tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="78594-308">The source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="78594-309">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="78594-310">/Dest:"destination"</span><span class="sxs-lookup"><span data-stu-id="78594-310">/Dest:"destination"</span></span>
<span data-ttu-id="78594-311">Specifica la destinazione in cui eseguire la copia.</span><span class="sxs-lookup"><span data-stu-id="78594-311">Specifies the destination to copy to.</span></span> <span data-ttu-id="78594-312">La destinazione può essere una directory di file system, un contenitore BLOB, una directory virtuale BLOB, una condivisione file di archiviazione, una directory file di archiviazione o una tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="78594-312">The destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="78594-313">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="78594-314">/Pattern:"file-pattern"</span><span class="sxs-lookup"><span data-stu-id="78594-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="78594-315">Specifica un criterio file indicante i file da copiare.</span><span class="sxs-lookup"><span data-stu-id="78594-315">Specifies a file pattern that indicates which files to copy.</span></span> <span data-ttu-id="78594-316">Il comportamento del parametro /Pattern è determinato dal percorso dei dati di origine e dalla presenza dell'opzione relativa alla modalità ricorsiva.</span><span class="sxs-lookup"><span data-stu-id="78594-316">The behavior of the /Pattern parameter is determined by the location of the source data, and the presence of the recursive mode option.</span></span> <span data-ttu-id="78594-317">È possibile specificare la modalità ricorsiva tramite l'opzione /S.</span><span class="sxs-lookup"><span data-stu-id="78594-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="78594-318">Se l'origine specificata è una directory nel file system, è possibile usare i caratteri jolly standard e viene cercata una corrispondenza del criterio del file specificato con i file inclusi nella directory.</span><span class="sxs-lookup"><span data-stu-id="78594-318">If the specified source is a directory in the file system, then standard wildcards are in effect, and the file pattern provided is matched against files within the directory.</span></span> <span data-ttu-id="78594-319">Se è specificata l'opzione /S, AzCopy cerca anche la corrispondenza del criterio specificato con tutti i file inclusi nelle sottocartelle della directory.</span><span class="sxs-lookup"><span data-stu-id="78594-319">If option /S is specified, then AzCopy also matches the specified pattern against all files in any subfolders beneath the directory.</span></span>

<span data-ttu-id="78594-320">Se l'origine specificata è un contenitore o una directory virtuale BLOB, non è possibile applicare i caratteri jolly.</span><span class="sxs-lookup"><span data-stu-id="78594-320">If the specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="78594-321">Se è specificata l'opzione /S, AzCopy interpreta i criteri del file specificato come prefisso del BLOB.</span><span class="sxs-lookup"><span data-stu-id="78594-321">If option /S is specified, then AzCopy interprets the specified file pattern as a blob prefix.</span></span> <span data-ttu-id="78594-322">Se non è specificata l'opzione /S, AzCopy cerca una corrispondenza esatta dei criteri con i nomi dei BLOB.</span><span class="sxs-lookup"><span data-stu-id="78594-322">If option /S is not specified, then AzCopy matches the file pattern against exact blob names.</span></span>

<span data-ttu-id="78594-323">Se l'origine specificata è una condivisione file di Azure, è necessario specificare il nome file esatto (ad esempio, abc.txt) per copiare un solo file oppure specificare l'opzione /S per copiare tutti i file nella condivisione in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="78594-323">If the specified source is an Azure file share, then you must either specify the exact file name, (e.g. abc.txt) to copy a single file, or specify option /S to copy all files in the share recursively.</span></span> <span data-ttu-id="78594-324">Se si specificano contemporaneamente il criterio del file e l'opzione /S, viene generato un errore.</span><span class="sxs-lookup"><span data-stu-id="78594-324">Attempting to specify both a file pattern and option /S together results in an error.</span></span>

<span data-ttu-id="78594-325">AzCopy utilizza la corrispondenza tra maiuscole e minuscole quando l’opzione /Source è un contenitore BLOB o una directory virtuale di BLOB e non utilizza la corrispondenza tra maiuscole e minuscole in tutti gli altri casi.</span><span class="sxs-lookup"><span data-stu-id="78594-325">AzCopy uses case-sensitive matching when the /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all the other cases.</span></span>

<span data-ttu-id="78594-326">Il criterio predefinito per i file, se non specificato in modo esplicito, è *.*</span><span class="sxs-lookup"><span data-stu-id="78594-326">The default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="78594-327">per un percorso del file system o un prefisso vuoto per un percorso di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="78594-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="78594-328">Non è consentito specificare più criteri file.</span><span class="sxs-lookup"><span data-stu-id="78594-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="78594-329">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="78594-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="78594-330">/DestKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="78594-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="78594-331">Specifica la chiave dell'account di archiviazione per la risorsa di destinazione.</span><span class="sxs-lookup"><span data-stu-id="78594-331">Specifies the storage account key for the destination resource.</span></span>

<span data-ttu-id="78594-332">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="78594-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="78594-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="78594-334">Specifica una firma di accesso condiviso con autorizzazioni di LETTURA e SCRITTURA per la destinazione (se applicabile).</span><span class="sxs-lookup"><span data-stu-id="78594-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for the destination (if applicable).</span></span> <span data-ttu-id="78594-335">Racchiudere la firma di accesso condiviso tra virgolette doppie, in quanto potrebbe contenere caratteri della riga di comando speciali.</span><span class="sxs-lookup"><span data-stu-id="78594-335">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="78594-336">Se la risorsa di destinazione è una tabella, una condivisione file o un contenitore BLOB, è possibile specificare questa opzione seguita dal token di accesso condiviso o specificare la firma di accesso condiviso come parte dell'URI della tabella, della condivisione file o del contenitore BLOB, senza questa opzione.</span><span class="sxs-lookup"><span data-stu-id="78594-336">If the destination resource is a blob container, file share or table, you can either specify this option followed by the SAS token, or you can specify the SAS as part of the destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="78594-337">Se l'origine e la destinazione sono entrambi BLOB, il BLOB di destinazione deve essere nello stesso account di archiviazione del BLOB di origine.</span><span class="sxs-lookup"><span data-stu-id="78594-337">If the source and destination are both blobs, then the destination blob must reside within the same storage account as the source blob.</span></span>

<span data-ttu-id="78594-338">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="78594-339">/SourceKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="78594-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="78594-340">Specifica la chiave dell'account di archiviazione per la risorsa di origine.</span><span class="sxs-lookup"><span data-stu-id="78594-340">Specifies the storage account key for the source resource.</span></span>

<span data-ttu-id="78594-341">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="78594-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="78594-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="78594-343">Specifica una firma di accesso condiviso con autorizzazioni di LETTURA ed ELENCO per l’origine (se applicabile).</span><span class="sxs-lookup"><span data-stu-id="78594-343">Specifies a Shared Access Signature with READ and LIST permissions for the source (if applicable).</span></span> <span data-ttu-id="78594-344">Racchiudere la firma di accesso condiviso tra virgolette doppie, in quanto potrebbe contenere caratteri della riga di comando speciali.</span><span class="sxs-lookup"><span data-stu-id="78594-344">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="78594-345">Se la risorsa di origine è un contenitore BLOB e non viene fornita né una chiave né una firma di accesso condiviso, il contenitore BLOB viene letto tramite accesso anonimo.</span><span class="sxs-lookup"><span data-stu-id="78594-345">If the source resource is a blob container, and neither a key nor a SAS is provided, then the blob container is read via anonymous access.</span></span>

<span data-ttu-id="78594-346">Se l'origine è una tabella o una condivisione file, è necessario specificare una chiave o una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="78594-346">If the source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="78594-347">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="78594-348">/S</span><span class="sxs-lookup"><span data-stu-id="78594-348">/S</span></span>
<span data-ttu-id="78594-349">Specifica la modalità ricorsiva per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="78594-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="78594-350">In modalità ricorsiva, AzCopy copia tutti i BLOB o i file corrispondenti al criterio di file specificato, inclusi quelli nelle sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="78594-350">In recursive mode, AzCopy copies all blobs or files that match the specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="78594-351">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="78594-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="78594-352">/BlobType:"block" | "page" | "append"</span><span class="sxs-lookup"><span data-stu-id="78594-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="78594-353">Specifica se il BLOB di destinazione è un BLOB in blocchi, un BLOB di pagine o un BLOB di accodamento.</span><span class="sxs-lookup"><span data-stu-id="78594-353">Specifies whether the destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="78594-354">Questa opzione è applicabile solo per l'upload di un BLOB.</span><span class="sxs-lookup"><span data-stu-id="78594-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="78594-355">In caso contrario, viene generato un errore.</span><span class="sxs-lookup"><span data-stu-id="78594-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="78594-356">Se la destinazione è un BLOB e questa opzione non è specificata, per impostazione predefinita AzCopy crea un BLOB in blocchi.</span><span class="sxs-lookup"><span data-stu-id="78594-356">If the destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="78594-357">**Applicabile a:** BLOB</span><span class="sxs-lookup"><span data-stu-id="78594-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="78594-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="78594-358">/CheckMD5</span></span>
<span data-ttu-id="78594-359">Calcola un hash MD5 per i dati scaricati e verifica che l'hash MD5 archiviato nella proprietà Content-MD5 del BLOB o del file corrisponda all'hash calcolato.</span><span class="sxs-lookup"><span data-stu-id="78594-359">Calculates an MD5 hash for downloaded data and verifies that the MD5 hash stored in the blob or file's Content-MD5 property matches the calculated hash.</span></span> <span data-ttu-id="78594-360">Il controllo MD5 è disattivato per impostazione predefinita, quindi è necessario specificare questa opzione per eseguire il controllo MD5 al download dei dati.</span><span class="sxs-lookup"><span data-stu-id="78594-360">The MD5 check is turned off by default, so you must specify this option to perform the MD5 check when downloading data.</span></span>

<span data-ttu-id="78594-361">Si noti che Archiviazione di Azure non garantisce che l'hash MD5 archiviato per il BLOB o il file sia aggiornato.</span><span class="sxs-lookup"><span data-stu-id="78594-361">Note that Azure Storage doesn't guarantee that the MD5 hash stored for the blob or file is up-to-date.</span></span> <span data-ttu-id="78594-362">È responsabilità del client aggiornare l'hash MD5 ogni volta che il BLOB o il file viene modificato.</span><span class="sxs-lookup"><span data-stu-id="78594-362">It is client's responsibility to update the MD5 whenever the blob or file is modified.</span></span>

<span data-ttu-id="78594-363">AzCopy imposta sempre la proprietà Content-MD5 per un BLOB o un file di Azure dopo averlo caricato nel servizio.</span><span class="sxs-lookup"><span data-stu-id="78594-363">AzCopy always sets the Content-MD5 property for an Azure blob or file after uploading it to the service.</span></span>  

<span data-ttu-id="78594-364">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="78594-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="78594-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="78594-365">/Snapshot</span></span>
<span data-ttu-id="78594-366">Indica se trasferire gli snapshot o meno.</span><span class="sxs-lookup"><span data-stu-id="78594-366">Indicates whether to transfer snapshots.</span></span> <span data-ttu-id="78594-367">Questa opzione è valida solo quando l'origine è un BLOB.</span><span class="sxs-lookup"><span data-stu-id="78594-367">This option is only valid when the source is a blob.</span></span>

<span data-ttu-id="78594-368">Gli snapshot di BLOB trasferiti vengono rinominati nel formato seguente: nome-BLOB (ora-snapshot).estensione.</span><span class="sxs-lookup"><span data-stu-id="78594-368">The transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="78594-369">Per impostazione predefinita, gli snapshot non vengono copiati.</span><span class="sxs-lookup"><span data-stu-id="78594-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="78594-370">**Applicabile a:** BLOB</span><span class="sxs-lookup"><span data-stu-id="78594-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="78594-371">/V:[verbose-log-file]</span><span class="sxs-lookup"><span data-stu-id="78594-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="78594-372">Esegue l'output dei messaggi di stato dettagliati in un file di log.</span><span class="sxs-lookup"><span data-stu-id="78594-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="78594-373">Per impostazione predefinita, al file di log dettagliato viene assegnato il nome AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="78594-373">By default, the verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="78594-374">Se per questa opzione si specifica un percorso di file esistente, al file viene aggiunto il log dettagliato.</span><span class="sxs-lookup"><span data-stu-id="78594-374">If you specify an existing file location for this option, the verbose log is appended to that file.</span></span>  

<span data-ttu-id="78594-375">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="78594-376">/Z:[journal-file-folder]</span><span class="sxs-lookup"><span data-stu-id="78594-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="78594-377">Specifica la cartella del file journal per la ripresa di un'operazione.</span><span class="sxs-lookup"><span data-stu-id="78594-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="78594-378">AzCopy supporta sempre la ripresa di un'operazione interrotta.</span><span class="sxs-lookup"><span data-stu-id="78594-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="78594-379">Se questa opzione non è specificata o se è specificata senza un percorso di cartella, AzCopy crea il file journal nel percorso predefinito, ovvero %LocalAppData%\Microsoft\Azure\AzCopy.</span><span class="sxs-lookup"><span data-stu-id="78594-379">If this option is not specified, or it is specified without a folder path, then AzCopy creates the journal file in the default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="78594-380">Ogni volta che si invia un comando ad AzCopy, l'utilità verifica se il file journal è presente nella cartella predefinita o in una cartella specificata dall'utente tramite questa opzione.</span><span class="sxs-lookup"><span data-stu-id="78594-380">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="78594-381">Se il file journal non viene trovato in tali percorsi, AzCopy considera l'operazione come nuova e quindi crea un nuovo file journal.</span><span class="sxs-lookup"><span data-stu-id="78594-381">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="78594-382">Se il file journal esiste, AzCopy verifica se la riga di comando di input corrisponde alla riga di comando nel file journal.</span><span class="sxs-lookup"><span data-stu-id="78594-382">If the journal file does exist, AzCopy checks whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="78594-383">Se le righe di comando corrispondono, AzCopy avvia la ripresa dell'operazione incompleta.</span><span class="sxs-lookup"><span data-stu-id="78594-383">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="78594-384">Se non corrispondono, viene chiesto se si vuole sovrascrivere il file journal per avviare una nuova operazione o annullare l'operazione corrente.</span><span class="sxs-lookup"><span data-stu-id="78594-384">If they do not match, you are prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="78594-385">Se l'operazione viene completata senza errori, il file journal viene eliminato.</span><span class="sxs-lookup"><span data-stu-id="78594-385">The journal file is deleted upon successful completion of the operation.</span></span>

<span data-ttu-id="78594-386">Si noti che la ripresa di un'operazione da un file journal creato da una versione precedente di AzCopy non è supportata.</span><span class="sxs-lookup"><span data-stu-id="78594-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="78594-387">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="78594-388">/@:"parameter-file"</span><span class="sxs-lookup"><span data-stu-id="78594-388">/@:"parameter-file"</span></span>
<span data-ttu-id="78594-389">Specifica un file contenente parametri.</span><span class="sxs-lookup"><span data-stu-id="78594-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="78594-390">AzCopy elabora i parametri nel file come se fossero stati specificati nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="78594-390">AzCopy processes the parameters in the file just as if they had been specified on the command line.</span></span>

<span data-ttu-id="78594-391">In un file di risposta è possibile specificare più parametri su una sola riga o specificare un parametro su ogni riga.</span><span class="sxs-lookup"><span data-stu-id="78594-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="78594-392">Si noti che un singolo parametro non può estendersi su più righe.</span><span class="sxs-lookup"><span data-stu-id="78594-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="78594-393">I file di risposta possono includere righe di commento che iniziano con il simbolo #.</span><span class="sxs-lookup"><span data-stu-id="78594-393">Response files can include comments lines that begin with the # symbol.</span></span>

<span data-ttu-id="78594-394">È possibile specificare più file di risposta.</span><span class="sxs-lookup"><span data-stu-id="78594-394">You can specify multiple response files.</span></span> <span data-ttu-id="78594-395">Tuttavia, tenere presente che AzCopy non supporta file di risposta annidati.</span><span class="sxs-lookup"><span data-stu-id="78594-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="78594-396">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="78594-397">/Y</span><span class="sxs-lookup"><span data-stu-id="78594-397">/Y</span></span>
<span data-ttu-id="78594-398">Elimina tutte le richieste di conferma di AzCopy.</span><span class="sxs-lookup"><span data-stu-id="78594-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="78594-399">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="78594-400">/L</span><span class="sxs-lookup"><span data-stu-id="78594-400">/L</span></span>
<span data-ttu-id="78594-401">Specifica solo un'operazione di elenco, non viene copiato alcun dato.</span><span class="sxs-lookup"><span data-stu-id="78594-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="78594-402">AzCopy interpreta l'utilizzo di questa opzione come una simulazione per l'esecuzione della riga di comando senza questa opzione /L e conta il numero di oggetti copiati. È possibile specificare contemporaneamente l'opzione /V per controllare quali oggetti vengono copiati nel log dettagliato.</span><span class="sxs-lookup"><span data-stu-id="78594-402">AzCopy interprets the using of this option as a simulation for running the command line without this option /L and counts how many objects are copied, you can specify option /V at the same time to check which objects are copied in the verbose log.</span></span>

<span data-ttu-id="78594-403">Il comportamento di questa opzione è determinato dal percorso dei dati di origine e dalla presenza dell'opzione relativa alla modalità ricorsiva /S e dell’opzione di modello file /Pattern.</span><span class="sxs-lookup"><span data-stu-id="78594-403">The behavior of this option is also determined by the location of the source data and the presence of the recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="78594-404">AzCopy richiede l'autorizzazione ELENCO e LETTURA per questo percorso di origine quando si utilizza questa opzione.</span><span class="sxs-lookup"><span data-stu-id="78594-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="78594-405">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="78594-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="78594-406">/MT</span><span class="sxs-lookup"><span data-stu-id="78594-406">/MT</span></span>
<span data-ttu-id="78594-407">Imposta l'ora dell'ultima modifica di un file scaricato sulla stessa ora del file o del BLOB di origine.</span><span class="sxs-lookup"><span data-stu-id="78594-407">Sets the downloaded file's last-modified time to be the same as the source blob or file's.</span></span>

<span data-ttu-id="78594-408">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="78594-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="78594-409">/XN</span><span class="sxs-lookup"><span data-stu-id="78594-409">/XN</span></span>
<span data-ttu-id="78594-410">Esclude una risorsa di origine più recente.</span><span class="sxs-lookup"><span data-stu-id="78594-410">Excludes a newer source resource.</span></span> <span data-ttu-id="78594-411">La risorsa non viene copiata se l'ora dell'ultima modifica dell'origine è uguale alla destinazione o più recente.</span><span class="sxs-lookup"><span data-stu-id="78594-411">The resource is not copied if the last modified time of the source is the same or newer than destination.</span></span>

<span data-ttu-id="78594-412">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="78594-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="78594-413">/XO</span><span class="sxs-lookup"><span data-stu-id="78594-413">/XO</span></span>
<span data-ttu-id="78594-414">Esclude una risorsa di origine meno recente.</span><span class="sxs-lookup"><span data-stu-id="78594-414">Excludes an older source resource.</span></span> <span data-ttu-id="78594-415">La risorsa non viene copiata se l'ora dell'ultima modifica dell'origine è uguale alla destinazione o meno recente.</span><span class="sxs-lookup"><span data-stu-id="78594-415">The resource is not copied if the last modified time of the source is the same or older than destination.</span></span>

<span data-ttu-id="78594-416">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="78594-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="78594-417">/A</span><span class="sxs-lookup"><span data-stu-id="78594-417">/A</span></span>
<span data-ttu-id="78594-418">Carica solo i file per i quali è impostato l'attributo Archive.</span><span class="sxs-lookup"><span data-stu-id="78594-418">Uploads only files that have the Archive attribute set.</span></span>

<span data-ttu-id="78594-419">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="78594-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="78594-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="78594-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="78594-421">Carica solo i file per i quali sono impostati gli attributi specificati.</span><span class="sxs-lookup"><span data-stu-id="78594-421">Uploads only files that have any of the specified attributes set.</span></span>

<span data-ttu-id="78594-422">Gli attributi disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="78594-422">Available attributes include:</span></span>

* <span data-ttu-id="78594-423">R = File di sola lettura</span><span class="sxs-lookup"><span data-stu-id="78594-423">R = Read-only files</span></span>
* <span data-ttu-id="78594-424">A = File pronti per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="78594-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="78594-425">S = File di sistema</span><span class="sxs-lookup"><span data-stu-id="78594-425">S = System files</span></span>
* <span data-ttu-id="78594-426">H = File nascosti</span><span class="sxs-lookup"><span data-stu-id="78594-426">H = Hidden files</span></span>
* <span data-ttu-id="78594-427">C = File compressi</span><span class="sxs-lookup"><span data-stu-id="78594-427">C = Compressed files</span></span>
* <span data-ttu-id="78594-428">N = File normali</span><span class="sxs-lookup"><span data-stu-id="78594-428">N = Normal files</span></span>
* <span data-ttu-id="78594-429">E = File crittografati</span><span class="sxs-lookup"><span data-stu-id="78594-429">E = Encrypted files</span></span>
* <span data-ttu-id="78594-430">T = File temporanei</span><span class="sxs-lookup"><span data-stu-id="78594-430">T = Temporary files</span></span>
* <span data-ttu-id="78594-431">O = File offline</span><span class="sxs-lookup"><span data-stu-id="78594-431">O = Offline files</span></span>
* <span data-ttu-id="78594-432">I = File non indicizzati</span><span class="sxs-lookup"><span data-stu-id="78594-432">I = Non-indexed files</span></span>

<span data-ttu-id="78594-433">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="78594-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="78594-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="78594-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="78594-435">Esclude i file per i quali sono impostati gli attributi specificati.</span><span class="sxs-lookup"><span data-stu-id="78594-435">Excludes files that have any of the specified attributes set.</span></span>

<span data-ttu-id="78594-436">Gli attributi disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="78594-436">Available attributes include:</span></span>

* <span data-ttu-id="78594-437">R = File di sola lettura</span><span class="sxs-lookup"><span data-stu-id="78594-437">R = Read-only files</span></span>
* <span data-ttu-id="78594-438">A = File pronti per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="78594-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="78594-439">S = File di sistema</span><span class="sxs-lookup"><span data-stu-id="78594-439">S = System files</span></span>
* <span data-ttu-id="78594-440">H = File nascosti</span><span class="sxs-lookup"><span data-stu-id="78594-440">H = Hidden files</span></span>
* <span data-ttu-id="78594-441">C = File compressi</span><span class="sxs-lookup"><span data-stu-id="78594-441">C = Compressed files</span></span>
* <span data-ttu-id="78594-442">N = File normali</span><span class="sxs-lookup"><span data-stu-id="78594-442">N = Normal files</span></span>
* <span data-ttu-id="78594-443">E = File crittografati</span><span class="sxs-lookup"><span data-stu-id="78594-443">E = Encrypted files</span></span>
* <span data-ttu-id="78594-444">T = File temporanei</span><span class="sxs-lookup"><span data-stu-id="78594-444">T = Temporary files</span></span>
* <span data-ttu-id="78594-445">O = File offline</span><span class="sxs-lookup"><span data-stu-id="78594-445">O = Offline files</span></span>
* <span data-ttu-id="78594-446">I = File non indicizzati</span><span class="sxs-lookup"><span data-stu-id="78594-446">I = Non-indexed files</span></span>

<span data-ttu-id="78594-447">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="78594-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="78594-448">/Delimiter:"delimiter"</span><span class="sxs-lookup"><span data-stu-id="78594-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="78594-449">Indica il delimitatore usato per delimitare le directory virtuali in un nome BLOB.</span><span class="sxs-lookup"><span data-stu-id="78594-449">Indicates the delimiter character used to delimit virtual directories in a blob name.</span></span>

<span data-ttu-id="78594-450">Per impostazione predefinita, AzCopy usa il carattere / come delimitatore.</span><span class="sxs-lookup"><span data-stu-id="78594-450">By default, AzCopy uses / as the delimiter character.</span></span> <span data-ttu-id="78594-451">Tuttavia, a questo scopo supporta anche l'uso di caratteri comuni, ad esempio @, # o %.</span><span class="sxs-lookup"><span data-stu-id="78594-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="78594-452">Se è necessario includere uno di questi caratteri speciali nella riga di comando, racchiudere il nome del file tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="78594-452">If you need to include one of these special characters on the command line, enclose the file name with double quotes.</span></span>

<span data-ttu-id="78594-453">Questa opzione si applica solo per il download di BLOB.</span><span class="sxs-lookup"><span data-stu-id="78594-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="78594-454">**Applicabile a:** BLOB</span><span class="sxs-lookup"><span data-stu-id="78594-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="78594-455">/NC:"number-of-concurrent-operations"</span><span class="sxs-lookup"><span data-stu-id="78594-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="78594-456">Specifica il numero di operazioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="78594-456">Specifies the number of concurrent operations.</span></span>

<span data-ttu-id="78594-457">Per impostazione predefinita, AzCopy avvia un determinato numero di operazioni simultanee per aumentare la velocità effettiva di trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="78594-457">AzCopy by default starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="78594-458">Si noti che un numero elevato di operazioni simultanee in un ambiente con una larghezza di banda ridotta potrebbe sovraccaricare la connessione di rete e impedire il corretto completamento delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="78594-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm the network connection and prevent the operations from fully completing.</span></span> <span data-ttu-id="78594-459">Limitare le operazioni simultanee in base alla larghezza di banda di rete effettivamente disponibile.</span><span class="sxs-lookup"><span data-stu-id="78594-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="78594-460">Il limite massimo per le operazioni simultanee è 512.</span><span class="sxs-lookup"><span data-stu-id="78594-460">The upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="78594-461">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="78594-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="78594-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="78594-463">Indica che la risorsa `source` è un BLOB disponibile nell'ambiente di sviluppo locale, in esecuzione nell'emulatore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="78594-463">Specifies that the `source` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="78594-464">**Applicabile a:** BLOB, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="78594-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="78594-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="78594-466">Indica che la risorsa `destination` è un BLOB disponibile nell'ambiente di sviluppo locale, in esecuzione nell'emulatore di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="78594-466">Specifies that the `destination` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="78594-467">**Applicabile a:** BLOB, tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="78594-468">/PKRS:"key1#key2#key3#..."</span><span class="sxs-lookup"><span data-stu-id="78594-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="78594-469">Divide l'intervallo di chiavi di partizione per consentire l'esportazione dei dati della tabella in parallelo, aumentando la velocità dell'operazione di esportazione.</span><span class="sxs-lookup"><span data-stu-id="78594-469">Splits the partition key range to enable exporting table data in parallel, which increases the speed of the export operation.</span></span>

<span data-ttu-id="78594-470">Se questa opzione non è specificata, AzCopy usa un solo thread per esportare le entità della tabella.</span><span class="sxs-lookup"><span data-stu-id="78594-470">If this option is not specified, then AzCopy uses a single thread to export table entities.</span></span> <span data-ttu-id="78594-471">Ad esempio, se l'utente specifica /PKRS:"aa#bb", AzCopy avvia tre operazioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="78594-471">For example, if the user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="78594-472">Ogni operazione esporta uno dei tre intervalli di chiavi di partizione, nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="78594-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="78594-473">[first-partition-key, aa)</span><span class="sxs-lookup"><span data-stu-id="78594-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="78594-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="78594-474">[aa, bb)</span></span>

  <span data-ttu-id="78594-475">[bb, last-partition-key]</span><span class="sxs-lookup"><span data-stu-id="78594-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="78594-476">**Applicabile a:** tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="78594-477">/SplitSize:"file-size"</span><span class="sxs-lookup"><span data-stu-id="78594-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="78594-478">Specifica la dimensione del file esportato diviso in MB, il valore minimo consentito è 32.</span><span class="sxs-lookup"><span data-stu-id="78594-478">Specifies the exported file split size in MB, the minimal value allowed is 32.</span></span>

<span data-ttu-id="78594-479">Se questa opzione non è specificata, AzCopy esporta i dati della tabella in un solo file.</span><span class="sxs-lookup"><span data-stu-id="78594-479">If this option is not specified, AzCopy exports table data to a single file.</span></span>

<span data-ttu-id="78594-480">Se i dati della tabella vengono esportati in un BLOB e le dimensioni del file esportato raggiungono il limite di 200 GB per le dimensioni del BLOB, AzCopy divide il file esportato, anche se questa opzione non viene specificata.</span><span class="sxs-lookup"><span data-stu-id="78594-480">If the table data is exported to a blob, and the exported file size reaches the 200 GB limit for blob size, then AzCopy splits the exported file, even if this option is not specified.</span></span>

<span data-ttu-id="78594-481">**Applicabile a:** tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="78594-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="78594-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="78594-483">Specifica il comportamento di importazione dei dati della tabella.</span><span class="sxs-lookup"><span data-stu-id="78594-483">Specifies the table data import behavior.</span></span>

* <span data-ttu-id="78594-484">InsertOrSkip - Ignora un'entità esistente oppure ne inserisce una nuova se non esiste nella tabella.</span><span class="sxs-lookup"><span data-stu-id="78594-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="78594-485">InsertOrMerge - Unisce un'entità esistente oppure ne inserisce una nuova se non esiste nella tabella.</span><span class="sxs-lookup"><span data-stu-id="78594-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="78594-486">InsertOrReplace - Sostituisce un'entità esistente oppure ne inserisce una nuova se non esiste nella tabella.</span><span class="sxs-lookup"><span data-stu-id="78594-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="78594-487">**Applicabile a:** tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="78594-488">/Manifest:"manifest-file"</span><span class="sxs-lookup"><span data-stu-id="78594-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="78594-489">Specifica il file manifesto per l'operazione di importazione ed esportazione della tabella.</span><span class="sxs-lookup"><span data-stu-id="78594-489">Specifies the manifest file for the table export and import operation.</span></span>

<span data-ttu-id="78594-490">Questa opzione è facoltativa durante l'operazione di esportazione. Se non viene specificata, AzCopy genera un file manifesto con il nome predefinito.</span><span class="sxs-lookup"><span data-stu-id="78594-490">This option is optional during the export operation, AzCopy generates a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="78594-491">Questa opzione è necessaria durante l'operazione di importazione per individuare i file di dati.</span><span class="sxs-lookup"><span data-stu-id="78594-491">This option is required during the import operation for locating the data files.</span></span>

<span data-ttu-id="78594-492">**Applicabile a:** tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="78594-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="78594-493">/SyncCopy</span></span>
<span data-ttu-id="78594-494">Indica se si desidera copiare BLOB o file in modo sincrono da un endpoint di Archiviazione di Azure a un altro.</span><span class="sxs-lookup"><span data-stu-id="78594-494">Indicates whether to synchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="78594-495">Per impostazione predefinita, AzCopy esegue la copia in modo asincrono sul lato server.</span><span class="sxs-lookup"><span data-stu-id="78594-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="78594-496">Specificare questa opzione per eseguire una copia sincrona, che scarica BLOB o file nella memoria locale e quindi li carica in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="78594-496">Specify this option to perform a synchronous copy, which downloads blobs or files to local memory and then uploads them to Azure Storage.</span></span>

<span data-ttu-id="78594-497">È possibile utilizzare questa opzione quando si copiano file all'interno dell'archiviazione BLOB o dell'archiviazione file oppure quando i file vengono copiati dall'archiviazione BLOB all'archiviazione file o viceversa.</span><span class="sxs-lookup"><span data-stu-id="78594-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage to File storage or vice versa.</span></span>

<span data-ttu-id="78594-498">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="78594-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="78594-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="78594-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="78594-500">Specifica il tipo di contenuto MIME per i BLOB o i file di destinazione.</span><span class="sxs-lookup"><span data-stu-id="78594-500">Specifies the MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="78594-501">Per impostazione predefinita, AzCopy imposta il tipo di contenuto per un BLOB o un file su application/octet-stream.</span><span class="sxs-lookup"><span data-stu-id="78594-501">AzCopy sets the content type for a blob or file to application/octet-stream by default.</span></span> <span data-ttu-id="78594-502">Se si desidera impostare il tipo di contenuto per tutti i BLOB o i file, è possibile specificare in modo esplicito un valore per questa opzione.</span><span class="sxs-lookup"><span data-stu-id="78594-502">You can set the content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="78594-503">Se si specifica questa opzione senza fornire un valore, AzCopy imposta il tipo di contenuto di ogni BLOB o file in base alla loro estensione.</span><span class="sxs-lookup"><span data-stu-id="78594-503">If you specify this option without a value, then AzCopy sets each blob or file's content type according to its file extension.</span></span>

<span data-ttu-id="78594-504">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="78594-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="78594-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="78594-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="78594-506">Specifica il formato del file di dati tabella esportato.</span><span class="sxs-lookup"><span data-stu-id="78594-506">Specifies the format of the table exported data file.</span></span>

<span data-ttu-id="78594-507">Se questa opzione non è specificata, per impostazione predefinita AzCopy esporta il file di dati tabella nel formato JSON.</span><span class="sxs-lookup"><span data-stu-id="78594-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="78594-508">**Applicabile a:** tabelle</span><span class="sxs-lookup"><span data-stu-id="78594-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="78594-509">Problemi noti e procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="78594-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="78594-510">Limitare le scritture simultanee durante la copia dei dati</span><span class="sxs-lookup"><span data-stu-id="78594-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="78594-511">Durante la copia di BLOB o file con AzCopy, tenere presente che altre applicazioni potrebbero modificare i dati mentre è in corso la copia.</span><span class="sxs-lookup"><span data-stu-id="78594-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="78594-512">Se possibile, assicurarsi che i dati copiati non vengano modificati durante l'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="78594-512">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="78594-513">Ad esempio, se si copia un file VHD associato a una macchina virtuale di Azure, verificare che altre applicazioni non stiano scrivendo nel file VHD durante la copia.</span><span class="sxs-lookup"><span data-stu-id="78594-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="78594-514">Un buon metodo per eseguire questa operazione è tramite leasing della risorsa da copiare.</span><span class="sxs-lookup"><span data-stu-id="78594-514">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="78594-515">In alternativa, è prima possibile creare uno snapshot del file VHD e quindi copiare lo snapshot.</span><span class="sxs-lookup"><span data-stu-id="78594-515">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="78594-516">Se non è possibile evitare che altre applicazioni scrivano nei BLOB o nei file durante l'operazione di copia, tenere presente che al termine del processo la parità delle risorse copiate con le risorse di origine potrebbe non essere completa.</span><span class="sxs-lookup"><span data-stu-id="78594-516">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="78594-517">Eseguire un'istanza di AzCopy su un computer.</span><span class="sxs-lookup"><span data-stu-id="78594-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="78594-518">AzCopy è progettato per massimizzare l'utilizzo della risorsa del computer per accelerare il trasferimento dei dati, è consigliabile eseguire solo un'istanza di AzCopy in un computer e specificare l'opzione `/NC` se sono necessarie più operazioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="78594-518">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="78594-519">Per ulteriori dettagli, digitare `AzCopy /?:NC` nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="78594-519">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="78594-520">Abilitare gli algoritmi MD5 conformi a FIPS per AzCopy quando si utilizzano gli algoritmi FIPS compatibili per crittografia, hash e firma.</span><span class="sxs-lookup"><span data-stu-id="78594-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="78594-521">AzCopy per impostazione predefinita utilizza l'implementazione .NET MD5 per calcolare l’algoritmo MD5 durante la copia di oggetti, ma esistono alcuni requisiti di sicurezza per cui è necessario abilitare in AzCopy l'impostazione MD5 conforme a FIPS.</span><span class="sxs-lookup"><span data-stu-id="78594-521">AzCopy by default uses .NET MD5 implementation to calculate the MD5 when copying objects, but there are some security requirements that need AzCopy to enable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="78594-522">È possibile creare un file app.config `AzCopy.exe.config` con la proprietà `AzureStorageUseV1MD5` e conservarlo con AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="78594-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="78594-523">Per la proprietà "AzureStorageUseV1MD5" • True: valore predefinito, AzCopy usa l'implementazione di .NET MD5.</span><span class="sxs-lookup"><span data-stu-id="78594-523">For property "AzureStorageUseV1MD5" • True - The default value, AzCopy uses .NET MD5 implementation.</span></span>
<span data-ttu-id="78594-524">• False: AzCopy usa l'algoritmo MD5 conforme a FIPS.</span><span class="sxs-lookup"><span data-stu-id="78594-524">• False – AzCopy uses FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="78594-525">Si noti che gli algoritmi conformi a FIPS sono disabilitati per impostazione predefinita nel computer Windows. Digitare secpol.msc nella finestra Esegui e selezionare questa opzione in Impostazione di sicurezza -> Criteri locali -> Opzioni di sicurezza -> Crittografia di sistema: utilizza algoritmi FIPS compatibili per crittografia, hash e firma.</span><span class="sxs-lookup"><span data-stu-id="78594-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78594-526">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="78594-526">Next steps</span></span>
<span data-ttu-id="78594-527">Per altre informazioni su Archiviazione di Azure e AzCopy, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="78594-527">For more information about Azure Storage and AzCopy, see the following resources:</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="78594-528">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="78594-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="78594-529">Introduzione ad Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="78594-529">Introduction to Azure Storage</span></span>](../storage-introduction.md)
* [<span data-ttu-id="78594-530">Come usare l'archiviazione BLOB da .NET</span><span class="sxs-lookup"><span data-stu-id="78594-530">How to use Blob storage from .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="78594-531">Come usare l'archiviazione file da .NET</span><span class="sxs-lookup"><span data-stu-id="78594-531">How to use File storage from .NET</span></span>](../storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="78594-532">Come usare l'archiviazione tabelle da .NET</span><span class="sxs-lookup"><span data-stu-id="78594-532">How to use Table storage from .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="78594-533">Come creare, gestire o eliminare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="78594-533">How to create, manage, or delete a storage account</span></span>](../storage-create-storage-account.md)
* [<span data-ttu-id="78594-534">Trasferire dati con AzCopy in Linux</span><span class="sxs-lookup"><span data-stu-id="78594-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="78594-535">Post del blog di Archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="78594-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="78594-536">Introduzione alla versione di anteprima della libreria per lo spostamento dei dati di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="78594-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="78594-537">AzCopy: introduzione alla copia sincrona e al tipo di contenuto personalizzato</span><span class="sxs-lookup"><span data-stu-id="78594-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="78594-538">AzCopy: annuncio della disponibilità per tutti di AzCopy 3.0 oltre alla versione di anteprima di AzCopy 4.0 con il supporto di tabelle e file</span><span class="sxs-lookup"><span data-stu-id="78594-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="78594-539">AzCopy: ottimizzazione per gli scenari di copia su larga scala</span><span class="sxs-lookup"><span data-stu-id="78594-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="78594-540">AzCopy:supporto per l'archiviazione con ridondanza geografica e accesso in lettura</span><span class="sxs-lookup"><span data-stu-id="78594-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="78594-541">AzCopy:trasferimento di dati con modalità riavviabile e token di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="78594-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="78594-542">AzCopy: uso del comando di copia dei BLOB tra account</span><span class="sxs-lookup"><span data-stu-id="78594-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="78594-543">AzCopy: Caricamento e download di file per BLOB di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="78594-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

