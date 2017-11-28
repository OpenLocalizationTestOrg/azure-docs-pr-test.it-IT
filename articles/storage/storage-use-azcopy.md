---
title: aaaCopy o lo spostamento dati tooAzure archiviazione con AzCopy in Windows | Documenti Microsoft
description: "Utilizzare hello AzCopy Windows utilità toomove o copia dati tooor dal blob, tabelle e contenuto del file. Copiare i dati tooAzure archiviazione da file locali, o copiare dati in o tra gli account di archiviazione. Migrare facilmente l'archiviazione di tooAzure di dati."
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
ms.openlocfilehash: a77db84c3a3e06f0ad4e87d02b14a5c62ed8d9ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-azcopy-on-windows"></a><span data-ttu-id="4483b-105">Trasferimento dati con hello AzCopy in Windows</span><span class="sxs-lookup"><span data-stu-id="4483b-105">Transfer data with hello AzCopy on Windows</span></span>
<span data-ttu-id="4483b-106">AzCopy è un'utilità della riga di comando progettata per la copia di dati tooand dall'archiviazione Blob di Microsoft Azure, File e tabella utilizzando i comandi semplici con prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="4483b-106">AzCopy is a command-line utility designed for copying data tooand from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="4483b-107">È possibile copiare dati da un oggetto tooanother all'interno dell'account di archiviazione o tra gli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4483b-107">You can copy data from one object tooanother within your storage account, or between storage accounts.</span></span>

<span data-ttu-id="4483b-108">Esistono due versioni di AzCopy che è possibile scaricare.</span><span class="sxs-lookup"><span data-stu-id="4483b-108">There are two versions of AzCopy that you can download.</span></span> <span data-ttu-id="4483b-109">AzCopy in Windows viene compilato con .NET Framework e offre opzioni della riga di comando in stile Windows.</span><span class="sxs-lookup"><span data-stu-id="4483b-109">AzCopy on Windows is built with .NET Framework, and offers Windows style command-line options.</span></span> <span data-ttu-id="4483b-110">[AzCopy in Linux](storage-use-azcopy-linux.md) viene compilato con .NET Framework per le piattaforme Linux e offre opzioni della riga di comando in stile POSIX.</span><span class="sxs-lookup"><span data-stu-id="4483b-110">[AzCopy on Linux](storage-use-azcopy-linux.md) is built with .NET Core Framework which targets Linux platforms offering POSIX style command-line options.</span></span> <span data-ttu-id="4483b-111">Questo articolo descrive AzCopy in Windows.</span><span class="sxs-lookup"><span data-stu-id="4483b-111">This article covers AzCopy on Windows.</span></span>

## <a name="download-and-install-azcopy"></a><span data-ttu-id="4483b-112">Scaricare e installare AzCopy</span><span class="sxs-lookup"><span data-stu-id="4483b-112">Download and install AzCopy</span></span>
### <a name="azcopy-on-windows"></a><span data-ttu-id="4483b-113">AzCopy in Windows</span><span class="sxs-lookup"><span data-stu-id="4483b-113">AzCopy on Windows</span></span>
<span data-ttu-id="4483b-114">Scaricare hello [versione più recente di AzCopy in Windows](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="4483b-114">Download hello [latest version of AzCopy on Windows](http://aka.ms/downloadazcopy).</span></span>

#### <a name="installation-on-windows"></a><span data-ttu-id="4483b-115">Installazione in Windows</span><span class="sxs-lookup"><span data-stu-id="4483b-115">Installation on Windows</span></span>
<span data-ttu-id="4483b-116">Dopo l'installazione di AzCopy in Windows tramite installazione guidata di hello, aprire una finestra di comando e passare toohello AzCopy directory di installazione nel computer in uso - dove hello `AzCopy.exe` eseguibile si trova.</span><span class="sxs-lookup"><span data-stu-id="4483b-116">After installing AzCopy on Windows using hello installer, open a command window and navigate toohello AzCopy installation directory on your computer - where hello `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="4483b-117">Se si desidera, è possibile aggiungere hello AzCopy tooyour sistema percorso di installazione.</span><span class="sxs-lookup"><span data-stu-id="4483b-117">If desired, you can add hello AzCopy installation location tooyour system path.</span></span> <span data-ttu-id="4483b-118">Per impostazione predefinita, AzCopy è installato troppo`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` o `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="4483b-118">By default, AzCopy is installed too`%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="4483b-119">Scrittura del primo comando AzCopy </span><span class="sxs-lookup"><span data-stu-id="4483b-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="4483b-120">sintassi di base per i comandi AzCopy Hello è:</span><span class="sxs-lookup"><span data-stu-id="4483b-120">hello basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="4483b-121">Hello seguenti esempi illustrano una varietà di scenari per la copia di dati tooand da BLOB di Microsoft Azure, file e tabelle.</span><span class="sxs-lookup"><span data-stu-id="4483b-121">hello following examples demonstrate a variety of scenarios for copying data tooand from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="4483b-122">Fare riferimento toohello [AzCopy parametri](#azcopy-parameters) sezione per una spiegazione dettagliata dei parametri di hello utilizzata in ogni esempio.</span><span class="sxs-lookup"><span data-stu-id="4483b-122">Refer toohello [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of hello parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="4483b-123">BLOB: scaricare</span><span class="sxs-lookup"><span data-stu-id="4483b-123">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="4483b-124">Scaricare un singolo BLOB</span><span class="sxs-lookup"><span data-stu-id="4483b-124">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="4483b-125">Si noti che se la cartella hello `C:\myfolder` non esiste, AzCopy la creerà e scaricare `abc.txt ` nella nuova cartella hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-125">Note that if hello folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into hello new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="4483b-126">Scaricare un singolo BLOB da un'area secondaria</span><span class="sxs-lookup"><span data-stu-id="4483b-126">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="4483b-127">È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="4483b-127">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="4483b-128">Scaricare tutti BLOB</span><span class="sxs-lookup"><span data-stu-id="4483b-128">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="4483b-129">Si supponga che segue hello BLOB si trovano nel contenitore specificato hello:</span><span class="sxs-lookup"><span data-stu-id="4483b-129">Assume hello following blobs reside in hello specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="4483b-130">Dopo un'operazione di download hello hello directory `C:\myfolder` includerà hello i seguenti file:</span><span class="sxs-lookup"><span data-stu-id="4483b-130">After hello download operation, hello directory `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="4483b-131">Se non si specifica l'opzione `/S`, non verrà scaricato alcun BLOB.</span><span class="sxs-lookup"><span data-stu-id="4483b-131">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="4483b-132">Scaricare i BLOB con il prefisso specificato</span><span class="sxs-lookup"><span data-stu-id="4483b-132">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="4483b-133">Si supponga che segue hello BLOB si trovano nel contenitore specificato hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-133">Assume hello following blobs reside in hello specified container.</span></span> <span data-ttu-id="4483b-134">Tutti i blob che iniziano con il prefisso hello `a` verranno scaricati:</span><span class="sxs-lookup"><span data-stu-id="4483b-134">All blobs beginning with hello prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="4483b-135">Dopo un'operazione di download hello hello cartella `C:\myfolder` includerà hello i seguenti file:</span><span class="sxs-lookup"><span data-stu-id="4483b-135">After hello download operation, hello folder `C:\myfolder` will include hello following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="4483b-136">prefisso Hello applica toohello directory virtuale, che costituisce hello prima parte del nome blob hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-136">hello prefix applies toohello virtual directory, which forms hello first part of hello blob name.</span></span> <span data-ttu-id="4483b-137">Nell'esempio hello illustrato in precedenza, la directory virtuale hello non corrisponde prefisso specificato hello, in modo che non è stato scaricato.</span><span class="sxs-lookup"><span data-stu-id="4483b-137">In hello example shown above, hello virtual directory does not match hello specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="4483b-138">Inoltre, se hello opzione `\S` non viene specificato, AzCopy non verranno scaricati tutti i BLOB.</span><span class="sxs-lookup"><span data-stu-id="4483b-138">In addition, if hello option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-hello-last-modified-time-of-exported-files-toobe-same-as-hello-source-blobs"></a><span data-ttu-id="4483b-139">Impostare l'ora dell'ultima modifica hello dei file esportati toobe stesso hello BLOB di origine</span><span class="sxs-lookup"><span data-stu-id="4483b-139">Set hello last-modified time of exported files toobe same as hello source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="4483b-140">È anche possibile escludere i BLOB da un'operazione di download hello in base all'ora ultima modifica.</span><span class="sxs-lookup"><span data-stu-id="4483b-140">You can also exclude blobs from hello download operation based on their last-modified time.</span></span> <span data-ttu-id="4483b-141">Ad esempio, se si desidera tooexclude BLOB la cui ultima modifica è hello uguale o più file di destinazione hello recente, aggiungere hello `/XN` opzione:</span><span class="sxs-lookup"><span data-stu-id="4483b-141">For example, if you want tooexclude blobs whose last modified time is hello same or newer than hello destination file, add hello `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="4483b-142">O se si desidera tooexclude BLOB la cui ultima modifica è hello stesso o meno i file di destinazione hello, aggiungere hello `/XO` opzione:</span><span class="sxs-lookup"><span data-stu-id="4483b-142">Or if you want tooexclude blobs whose last modified time is hello same or older than hello destination file, add hello `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="4483b-143">BLOB: caricare</span><span class="sxs-lookup"><span data-stu-id="4483b-143">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="4483b-144">Caricare un singolo file</span><span class="sxs-lookup"><span data-stu-id="4483b-144">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="4483b-145">Se hello contenitore di destinazione specificato non esiste, AzCopy verrà creato e caricare file hello al suo interno.</span><span class="sxs-lookup"><span data-stu-id="4483b-145">If hello specified destination container does not exist, AzCopy will create it and upload hello file into it.</span></span>

### <a name="upload-single-file-toovirtual-directory"></a><span data-ttu-id="4483b-146">Caricare file singoli toovirtual directory</span><span class="sxs-lookup"><span data-stu-id="4483b-146">Upload single file toovirtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="4483b-147">Se hello specificato una directory virtuale non esiste, AzCopy caricherà hello file tooinclude hello directory virtuale nel nome (*ad esempio*, `vd/abc.txt` nell'esempio hello sopra).</span><span class="sxs-lookup"><span data-stu-id="4483b-147">If hello specified virtual directory does not exist, AzCopy will upload hello file tooinclude hello virtual directory in its name (*e.g.*, `vd/abc.txt` in hello example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="4483b-148">Caricare tutti i file</span><span class="sxs-lookup"><span data-stu-id="4483b-148">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="4483b-149">Specifica l'opzione `/S` contenuto hello caricamenti di hello specificato directory tooBlob archiviazione in modo ricorsivo, vale a dire che tutte le sottocartelle e i relativi file verranno caricati anche.</span><span class="sxs-lookup"><span data-stu-id="4483b-149">Specifying option `/S` uploads hello contents of hello specified directory tooBlob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="4483b-150">Ad esempio, si supponga che segue hello file si trovano nella cartella `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="4483b-150">For instance, assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="4483b-151">Dopo un'operazione di caricamento hello contenitore hello includerà hello i seguenti file:</span><span class="sxs-lookup"><span data-stu-id="4483b-151">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="4483b-152">Se non si specifica l'opzione `/S`, AzCopy non caricherà i file in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="4483b-152">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="4483b-153">Dopo un'operazione di caricamento hello contenitore hello includerà hello i seguenti file:</span><span class="sxs-lookup"><span data-stu-id="4483b-153">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="4483b-154">Caricare i file corrispondenti ai criteri specificati</span><span class="sxs-lookup"><span data-stu-id="4483b-154">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="4483b-155">Si supponga che segue hello file si trovano nella cartella `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="4483b-155">Assume hello following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="4483b-156">Dopo un'operazione di caricamento hello contenitore hello includerà hello i seguenti file:</span><span class="sxs-lookup"><span data-stu-id="4483b-156">After hello upload operation, hello container will include hello following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="4483b-157">Se non si specifica l'opzione `/S`, AzCopy caricherà solo i BLOB che non si trovano in una directory virtuale:</span><span class="sxs-lookup"><span data-stu-id="4483b-157">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-hello-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="4483b-158">Specificare hello tipo di contenuto MIME di un blob di destinazione</span><span class="sxs-lookup"><span data-stu-id="4483b-158">Specify hello MIME content type of a destination blob</span></span>
<span data-ttu-id="4483b-159">Per impostazione predefinita, AzCopy Imposta tipo di contenuto di un blob di destinazione hello troppo`application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="4483b-159">By default, AzCopy sets hello content type of a destination blob too`application/octet-stream`.</span></span> <span data-ttu-id="4483b-160">A partire dalla versione 3.1.0, è possibile specificare in modo esplicito tipo di contenuto tramite l'opzione hello hello `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="4483b-160">Beginning with version 3.1.0, you can explicitly specify hello content type via hello option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="4483b-161">Questa sintassi Imposta tipo di contenuto hello per tutti i BLOB in un'operazione di caricamento.</span><span class="sxs-lookup"><span data-stu-id="4483b-161">This syntax sets hello content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="4483b-162">Se si specifica `/SetContentType` senza un valore, quindi AzCopy imposterà ogni blob o il tipo di contenuto del file in base a tooits estensione di file.</span><span class="sxs-lookup"><span data-stu-id="4483b-162">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="4483b-163">BLOB: copiare</span><span class="sxs-lookup"><span data-stu-id="4483b-163">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="4483b-164">Copiare un BLOB all'interno di un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4483b-164">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="4483b-165">Quando si copia un BLOB all'interno di un account di archiviazione, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4483b-165">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="4483b-166">Copiare un singolo BLOB tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4483b-166">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="4483b-167">Quando si copia un BLOB tra account di archiviazione, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4483b-167">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-tooprimary-region"></a><span data-ttu-id="4483b-168">Copiare blob singolo dall'area tooprimary area secondaria</span><span class="sxs-lookup"><span data-stu-id="4483b-168">Copy single blob from secondary region tooprimary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="4483b-169">È necessario che sia abilitata l'archiviazione con ridondanza geografica con accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="4483b-169">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="4483b-170">Copiare un singolo BLOB e i relativi snapshot tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4483b-170">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="4483b-171">Dopo un'operazione di copia hello contenitore di destinazione hello includerà blob hello e i relativi snapshot.</span><span class="sxs-lookup"><span data-stu-id="4483b-171">After hello copy operation, hello target container will include hello blob and its snapshots.</span></span> <span data-ttu-id="4483b-172">Se il blob di hello esempio hello precedente contiene due snapshot, il contenitore di hello includerà seguente hello blob e snapshot:</span><span class="sxs-lookup"><span data-stu-id="4483b-172">Assuming hello blob in hello example above has two snapshots, hello container will include hello following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="4483b-173">Copiare in modo sincrono i BLOB tra account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4483b-173">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="4483b-174">Per impostazione predefinita, AzCopy copia i dati tra due endpoint di archiviazione in modo asincrono.</span><span class="sxs-lookup"><span data-stu-id="4483b-174">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="4483b-175">Pertanto, operazione di copia hello verrà eseguito in background hello usando la capacità della larghezza di banda di riserva che non dispone di alcun contratto di servizio in termini di velocità con cui verrà copiato un blob e AzCopy verificherà periodicamente lo stato di copia hello fino a quando non hello copia viene completata o non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="4483b-175">Therefore, hello copy operation will run in hello background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check hello copy status until hello copying is completed or failed.</span></span>

<span data-ttu-id="4483b-176">Hello `/SyncCopy` opzione assicura che l'operazione di copia hello otterranno velocità coerente.</span><span class="sxs-lookup"><span data-stu-id="4483b-176">hello `/SyncCopy` option ensures that hello copy operation will get consistent speed.</span></span> <span data-ttu-id="4483b-177">AzCopy esegue copia sincrono hello scaricando BLOB hello toocopy da hello specificato memoria toolocal di origine e quindi caricarli toohello destinazione di archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="4483b-177">AzCopy performs hello synchronous copy by downloading hello blobs toocopy from hello specified source toolocal memory, and then uploading them toohello Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="4483b-178">`/SyncCopy`potrebbe generare ulteriore uscita costo copia tooasynchronous confrontati, hello approccio consigliato è toouse questa opzione in una macchina virtuale di Azure in hello stessa area del costo di uscita origine tooavoid account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4483b-178">`/SyncCopy` might generate additional egress cost compared tooasynchronous copy, hello recommended approach is toouse this option in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="4483b-179">File: scaricare</span><span class="sxs-lookup"><span data-stu-id="4483b-179">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="4483b-180">Scaricare un singolo file</span><span class="sxs-lookup"><span data-stu-id="4483b-180">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="4483b-181">Se è specificato l'origine è una condivisione di file di Azure, quindi è necessario specificare il nome di file esatto hello, hello (*ad esempio* `abc.txt`) toodownload un singolo file, oppure specificare l'opzione `/S` toodownload tutti i file nella condivisione di hello in modo ricorsivo.</span><span class="sxs-lookup"><span data-stu-id="4483b-181">If hello specified source is an Azure file share, then you must either specify hello exact file name, (*e.g.* `abc.txt`) toodownload a single file, or specify option `/S` toodownload all files in hello share recursively.</span></span> <span data-ttu-id="4483b-182">Il tentativo di toospecify un modello di file e l'opzione `/S` insieme si verificherà un errore.</span><span class="sxs-lookup"><span data-stu-id="4483b-182">Attempting toospecify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="4483b-183">Scaricare tutti i file</span><span class="sxs-lookup"><span data-stu-id="4483b-183">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="4483b-184">Le cartelle vuote non verranno scaricate.</span><span class="sxs-lookup"><span data-stu-id="4483b-184">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="4483b-185">File: caricare</span><span class="sxs-lookup"><span data-stu-id="4483b-185">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="4483b-186">Caricare un singolo file</span><span class="sxs-lookup"><span data-stu-id="4483b-186">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="4483b-187">Caricare tutti i file</span><span class="sxs-lookup"><span data-stu-id="4483b-187">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="4483b-188">Le cartelle vuote non verranno caricate.</span><span class="sxs-lookup"><span data-stu-id="4483b-188">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="4483b-189">Caricare i file corrispondenti ai criteri specificati</span><span class="sxs-lookup"><span data-stu-id="4483b-189">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="4483b-190">File: copia</span><span class="sxs-lookup"><span data-stu-id="4483b-190">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="4483b-191">Copiare tra condivisioni file</span><span class="sxs-lookup"><span data-stu-id="4483b-191">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="4483b-192">Quando si copia un file tra condivisioni file, viene eseguita un'operazione di [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx).</span><span class="sxs-lookup"><span data-stu-id="4483b-192">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-tooblob"></a><span data-ttu-id="4483b-193">Copiare da tooblob condivisione file</span><span class="sxs-lookup"><span data-stu-id="4483b-193">Copy from file share tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="4483b-194">Quando si copia un file da tooblob di condivisione file, un [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) viene eseguita l'operazione.</span><span class="sxs-lookup"><span data-stu-id="4483b-194">When you copy a file from file share tooblob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-toofile-share"></a><span data-ttu-id="4483b-195">Copiare da blob toofile condivisione</span><span class="sxs-lookup"><span data-stu-id="4483b-195">Copy from blob toofile share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="4483b-196">Quando si copia un file dalla condivisione toofile blob, un [copia sul lato server](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) viene eseguita l'operazione.</span><span class="sxs-lookup"><span data-stu-id="4483b-196">When you copy a file from blob toofile share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="4483b-197">Copiare file in modo sincrono</span><span class="sxs-lookup"><span data-stu-id="4483b-197">Synchronously copy files</span></span>
<span data-ttu-id="4483b-198">È possibile specificare hello `/SyncCopy` opzione toocopy dati da archiviazione di File tooFile, archiviazione, dall'archiviazione di File tooBlob, archiviazione e dall'archiviazione Blob tooFile archiviazione in modo sincrono, AzCopy esegue questa operazione di download di memoria di toolocal hello origine dati e di caricarlo toodestination nuovamente.</span><span class="sxs-lookup"><span data-stu-id="4483b-198">You can specify hello `/SyncCopy` option toocopy data from File Storage tooFile Storage, from File Storage tooBlob Storage and from Blob Storage tooFile Storage synchronously, AzCopy does this by downloading hello source data toolocal memory and upload it again toodestination.</span></span> <span data-ttu-id="4483b-199">Verranno applicati i costi in uscita standard.</span><span class="sxs-lookup"><span data-stu-id="4483b-199">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="4483b-200">Durante la copia da archiviazione di File tooBlob archiviazione, è di tipo di blob predefinito hello blob in blocchi, l'utente può specificare l'opzione `/BlobType:page` toochange hello tipo di blob di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4483b-200">When copying from File Storage tooBlob Storage, hello default blob type is block blob, user can specify option `/BlobType:page` toochange hello destination blob type.</span></span>

<span data-ttu-id="4483b-201">Si noti che `/SyncCopy` potrebbe generare uscita ulteriore costi confronto tooasynchronous copia, l'approccio consigliato hello è toouse hello di questa opzione nella macchina virtuale di Azure in hello stessa area del costo di uscita origine tooavoid account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4483b-201">Note that `/SyncCopy` might generate additional egress cost comparing tooasynchronous copy, hello recommended approach is toouse this option in hello Azure VM which is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="4483b-202">Tabella: esportare</span><span class="sxs-lookup"><span data-stu-id="4483b-202">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="4483b-203">Esportare una tabella</span><span class="sxs-lookup"><span data-stu-id="4483b-203">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="4483b-204">AzCopy scrive una cartella di destinazione specificato toohello file manifesto.</span><span class="sxs-lookup"><span data-stu-id="4483b-204">AzCopy writes a manifest file toohello specified destination folder.</span></span> <span data-ttu-id="4483b-205">file manifesto Hello viene usato nei file di dati necessari hello hello importazione processo toolocate ed eseguire la convalida dei dati.</span><span class="sxs-lookup"><span data-stu-id="4483b-205">hello manifest file is used in hello import process toolocate hello necessary data files and perform data validation.</span></span> <span data-ttu-id="4483b-206">file manifesto Hello utilizza hello convenzione di denominazione seguente per impostazione predefinita:</span><span class="sxs-lookup"><span data-stu-id="4483b-206">hello manifest file uses hello following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="4483b-207">È inoltre possibile specificare opzione hello `/Manifest:<manifest file name>` tooset nome del file manifesto hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-207">User can also specify hello option `/Manifest:<manifest file name>` tooset hello manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="4483b-208">Dividere l'esportazione in più file</span><span class="sxs-lookup"><span data-stu-id="4483b-208">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="4483b-209">AzCopy utilizza un *l'indice di volume* in hello suddividere i dati di nomi di file toodistinguish più file.</span><span class="sxs-lookup"><span data-stu-id="4483b-209">AzCopy uses a *volume index* in hello split data file names toodistinguish multiple files.</span></span> <span data-ttu-id="4483b-210">indice di volume Hello è costituito da due parti, un *indice intervalli di chiavi di partizione* e *split file indice*.</span><span class="sxs-lookup"><span data-stu-id="4483b-210">hello volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="4483b-211">Entrambi gli indici sono in base zero.</span><span class="sxs-lookup"><span data-stu-id="4483b-211">Both indexes are zero-based.</span></span>

<span data-ttu-id="4483b-212">indice di intervalli di chiavi di partizione Hello sarà pari a 0 se l'utente non specifica l'opzione `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="4483b-212">hello partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="4483b-213">Si supponga, ad esempio, AzCopy genera due file di dati dopo che l'utente hello specifica l'opzione `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="4483b-213">For instance, suppose AzCopy generates two data files after hello user specifies option `/SplitSize`.</span></span> <span data-ttu-id="4483b-214">potrebbe essere Hello risultante i nomi di file di dati:</span><span class="sxs-lookup"><span data-stu-id="4483b-214">hello resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="4483b-215">Si noti che hello valore minimo possibile per l'opzione `/SplitSize` 32 MB.</span><span class="sxs-lookup"><span data-stu-id="4483b-215">Note that hello minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="4483b-216">Se hello specificato di destinazione è l'archiviazione Blob, AzCopy verrà dividere il file di dati hello una volta la dimensioni raggiunge hello blob dimensione massima consentita (200GB), indipendentemente dall'opzione se `/SplitSize` è stato specificato dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-216">If hello specified destination is Blob storage, AzCopy will split hello data file once its sizes reaches hello blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by hello user.</span></span>

### <a name="export-table-toojson-or-csv-data-file-format"></a><span data-ttu-id="4483b-217">Esportare tooJSON tabella o un formato di file di dati CSV</span><span class="sxs-lookup"><span data-stu-id="4483b-217">Export table tooJSON or CSV data file format</span></span>
<span data-ttu-id="4483b-218">AzCopy per impostazione predefinita consente di esportare i file di dati di tabelle tooJSON.</span><span class="sxs-lookup"><span data-stu-id="4483b-218">AzCopy by default exports tables tooJSON data files.</span></span> <span data-ttu-id="4483b-219">È possibile specificare l'opzione hello `/PayloadFormat:JSON|CSV` tabelle hello tooexport come JSON o CSV.</span><span class="sxs-lookup"><span data-stu-id="4483b-219">You can specify hello option `/PayloadFormat:JSON|CSV` tooexport hello tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="4483b-220">Quando si specifica il formato di payload di hello CSV, AzCopy genererà inoltre un file di schema con estensione `.schema.csv` per ogni file di dati.</span><span class="sxs-lookup"><span data-stu-id="4483b-220">When specifying hello CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="4483b-221">Esportare entità tabella simultaneamente</span><span class="sxs-lookup"><span data-stu-id="4483b-221">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="4483b-222">AzCopy avvierà entità tooexport operazioni simultanee all'utente di hello specifica l'opzione `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="4483b-222">AzCopy will start concurrent operations tooexport entities when hello user specifies option `/PKRS`.</span></span> <span data-ttu-id="4483b-223">Ogni operazione esporta un intervallo di chiavi di partizione.</span><span class="sxs-lookup"><span data-stu-id="4483b-223">Each operation exports one partition key range.</span></span>

<span data-ttu-id="4483b-224">Si noti che il numero di hello di operazioni simultanee anche viene controllato dall'opzione `/NC`.</span><span class="sxs-lookup"><span data-stu-id="4483b-224">Note that hello number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="4483b-225">AzCopy utilizza il numero di hello di processori core come valore predefinito hello `/NC` quando si copiano le entità tabella, anche se `/NC` non è stato specificato.</span><span class="sxs-lookup"><span data-stu-id="4483b-225">AzCopy uses hello number of core processors as hello default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="4483b-226">Quando utente hello specifica l'opzione `/PKRS`, AzCopy utilizza hello minore del numero di hello due valori - partizione intervalli di chiavi e operazioni simultanee in modo implicito o esplicito specificate - toodetermine hello di toostart operazioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="4483b-226">When hello user specifies option `/PKRS`, AzCopy uses hello smaller of hello two values - partition key ranges versus implicitly or explicitly specified concurrent operations - toodetermine hello number of concurrent operations toostart.</span></span> <span data-ttu-id="4483b-227">Per ulteriori informazioni, digitare `AzCopy /?:NC` nella riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-227">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="export-table-tooblob"></a><span data-ttu-id="4483b-228">Esportazione tabella tooblob</span><span class="sxs-lookup"><span data-stu-id="4483b-228">Export table tooblob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="4483b-229">AzCopy genererà un file di dati JSON in un contenitore blob hello con convenzione di denominazione seguente:</span><span class="sxs-lookup"><span data-stu-id="4483b-229">AzCopy will generate a JSON data file into hello blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="4483b-230">file di dati JSON Hello generato segue il formato di payload hello per metadati minimi.</span><span class="sxs-lookup"><span data-stu-id="4483b-230">hello generated JSON data file follows hello payload format for minimal metadata.</span></span> <span data-ttu-id="4483b-231">Per i dettagli su questo formato di payload, vedere [Formato di payload per le operazioni del servizio tabelle](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="4483b-231">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="4483b-232">Si noti che quando si esportano tabelle tooblobs, AzCopy sarà di scaricare i file di dati temporanei toolocal entità tabella hello e quindi caricare tali blob toohello entità.</span><span class="sxs-lookup"><span data-stu-id="4483b-232">Note that when exporting tables tooblobs, AzCopy will download hello Table entities toolocal temporary data files and then upload those entities toohello blob.</span></span> <span data-ttu-id="4483b-233">Questi file di dati temporanei vengono inseriti nella cartella di file hello giornale di registrazione con il percorso predefinito di hello "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", è possibile specificare l'opzione/toochange [cartella di file journal] z: hello percorso della cartella file journal e pertanto modificare percorso dei file di dati temporanei hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-233">These temporary data files are put into hello journal file folder with hello default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] toochange hello journal file folder location and thus change hello temporary data files location.</span></span> <span data-ttu-id="4483b-234">dati temporanei, le dimensioni dei file viene stabilita delle entità di tabella dimensioni e hello che è specificato con /SplitSize opzione hello, anche se il file di dati temporanei hello nel disco locale verrà eliminato immediatamente dopo che è stato Hello caricate toohello blob, assicurarsi che si disporre di sufficiente toostore di spazio su disco locale questi file di dati temporanei vengono eliminati.</span><span class="sxs-lookup"><span data-stu-id="4483b-234">hello temporary data files' size is decided by your table entities' size and hello size you specified with hello option /SplitSize, although hello temporary data file in local disk will be deleted instantly once it has been uploaded toohello blob, please make sure you have enough local disk space toostore these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="4483b-235">Tabella: importare</span><span class="sxs-lookup"><span data-stu-id="4483b-235">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="4483b-236">Importare una tabella</span><span class="sxs-lookup"><span data-stu-id="4483b-236">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="4483b-237">opzione Hello `/EntityOperation` indica come entità tooinsert in hello tabella.</span><span class="sxs-lookup"><span data-stu-id="4483b-237">hello option `/EntityOperation` indicates how tooinsert entities into hello table.</span></span> <span data-ttu-id="4483b-238">I valori possibili sono:</span><span class="sxs-lookup"><span data-stu-id="4483b-238">Possible values are:</span></span>

* <span data-ttu-id="4483b-239">`InsertOrSkip`: Ignora un'entità esistente o inserisce una nuova entità se non esiste nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-239">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="4483b-240">`InsertOrMerge`: Unisce un'entità esistente o inserisce una nuova entità se non esiste nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-240">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="4483b-241">`InsertOrReplace`: Sostituisce un'entità esistente o inserisce una nuova entità se non esiste nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-241">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="4483b-242">Si noti che non è possibile specificare l'opzione `/PKRS` in uno scenario di importazione hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-242">Note that you cannot specify option `/PKRS` in hello import scenario.</span></span> <span data-ttu-id="4483b-243">Diversamente dallo scenario di esportazione hello, in cui è necessario specificare l'opzione `/PKRS` toostart operazioni simultanee, AzCopy per impostazione predefinita avvia operazioni simultanee quando si importa una tabella.</span><span class="sxs-lookup"><span data-stu-id="4483b-243">Unlike hello export scenario, in which you must specify option `/PKRS` toostart concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="4483b-244">numero di operazioni simultanee di avvio predefinito di Hello è uguale toohello numero di processori core; Tuttavia, è possibile specificare un numero diverso di simultanee con l'opzione `/NC`.</span><span class="sxs-lookup"><span data-stu-id="4483b-244">hello default number of concurrent operations started is equal toohello number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="4483b-245">Per ulteriori informazioni, digitare `AzCopy /?:NC` nella riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-245">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

<span data-ttu-id="4483b-246">Si noti che AzCopy supporta solo l'importazione per JSON, non per CSV.</span><span class="sxs-lookup"><span data-stu-id="4483b-246">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="4483b-247">AzCopy non supporta l'importazione di tabelle da file JSON e file manifesto creati dall'utente.</span><span class="sxs-lookup"><span data-stu-id="4483b-247">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="4483b-248">Entrambi questi file devono provenire da un'esportazione di tabella di AzCopy.</span><span class="sxs-lookup"><span data-stu-id="4483b-248">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="4483b-249">tooavoid errori, non modificare hello esportata JSON o un file manifesto.</span><span class="sxs-lookup"><span data-stu-id="4483b-249">tooavoid errors, please do not modify hello exported JSON or manifest file.</span></span>

### <a name="import-entities-tootable-using-blobs"></a><span data-ttu-id="4483b-250">Importazione di entità tootable tramite i BLOB</span><span class="sxs-lookup"><span data-stu-id="4483b-250">Import entities tootable using blobs</span></span>
<span data-ttu-id="4483b-251">Si supponga che un contenitore Blob contenuto seguente hello: file oggetto JSON che rappresenta una tabella di Azure e il relativo file manifesto.</span><span class="sxs-lookup"><span data-stu-id="4483b-251">Assume a Blob container contains hello following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="4483b-252">È possibile eseguire hello seguenti entità tooimport comando in una tabella utilizzando il file manifesto di hello in tale contenitore blob:</span><span class="sxs-lookup"><span data-stu-id="4483b-252">You can run hello following command tooimport entities into a table using hello manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="4483b-253">Altre funzionalità di AzCopy</span><span class="sxs-lookup"><span data-stu-id="4483b-253">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-hello-destination"></a><span data-ttu-id="4483b-254">Copia solo i dati che non esistono nella destinazione hello</span><span class="sxs-lookup"><span data-stu-id="4483b-254">Only copy data that doesn't exist in hello destination</span></span>
<span data-ttu-id="4483b-255">Hello `/XO` e `/XN` parametri consentono tooexclude le risorse dell'origine o meno recente viene copiato, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="4483b-255">hello `/XO` and `/XN` parameters allow you tooexclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="4483b-256">Se si desidera solo le risorse dell'origine toocopy che non sono presenti nella destinazione hello, è possibile specificare entrambi i parametri nel comando AzCopy hello:</span><span class="sxs-lookup"><span data-stu-id="4483b-256">If you only want toocopy source resources that don't exist in hello destination, you can specify both parameters in hello AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="4483b-257">Si noti che questo non è supportato quando hello origine o destinazione è una tabella.</span><span class="sxs-lookup"><span data-stu-id="4483b-257">Note that this is not supported when either hello source or destination is a table.</span></span>

### <a name="use-a-response-file-toospecify-command-line-parameters"></a><span data-ttu-id="4483b-258">Utilizzare un parametri della riga di comando toospecify del file di risposta</span><span class="sxs-lookup"><span data-stu-id="4483b-258">Use a response file toospecify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="4483b-259">È possibile includere i parametri della riga di comando di AzCopy in un file di risposta.</span><span class="sxs-lookup"><span data-stu-id="4483b-259">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="4483b-260">I processi di AzCopy hello parametri nel file hello come se fossero stati specificati nella riga di comando hello, eseguire una sostituzione diretta con contenuto hello del file hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-260">AzCopy processes hello parameters in hello file as if they had been specified on hello command line, performing a direct substitution with hello contents of hello file.</span></span>

<span data-ttu-id="4483b-261">Si supponga che un file di risposta denominato `copyoperation.txt`, che contiene hello seguenti righe.</span><span class="sxs-lookup"><span data-stu-id="4483b-261">Assume a response file named `copyoperation.txt`, that contains hello following lines.</span></span> <span data-ttu-id="4483b-262">Ogni parametro di AzCopy può essere specificato su una singola riga</span><span class="sxs-lookup"><span data-stu-id="4483b-262">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="4483b-263">o su righe separate:</span><span class="sxs-lookup"><span data-stu-id="4483b-263">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="4483b-264">AzCopy non riuscirà se il parametro hello si divide in due righe, come illustrato di seguito per hello `/sourcekey` parametro:</span><span class="sxs-lookup"><span data-stu-id="4483b-264">AzCopy will fail if you split hello parameter across two lines, as shown here for hello `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-toospecify-command-line-parameters"></a><span data-ttu-id="4483b-265">Utilizzare più risposta file toospecify parametri della riga di comando</span><span class="sxs-lookup"><span data-stu-id="4483b-265">Use multiple response files toospecify command-line parameters</span></span>
<span data-ttu-id="4483b-266">Si supponga che siano presenti un file di risposta denominato `source.txt` , che specifica un contenitore di origine:</span><span class="sxs-lookup"><span data-stu-id="4483b-266">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="4483b-267">E un file di risposta denominato `dest.txt` che specifica una cartella di destinazione nel file system di hello:</span><span class="sxs-lookup"><span data-stu-id="4483b-267">And a response file named `dest.txt` that specifies a destination folder in hello file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="4483b-268">E un file di risposta denominato `options.txt` , che specifica le opzioni per AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4483b-268">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="4483b-269">toocall AzCopy con questi file di risposta, di cui si trovano tutti in una directory `C:\responsefiles`, utilizzare questo comando:</span><span class="sxs-lookup"><span data-stu-id="4483b-269">toocall AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="4483b-270">AzCopy elabora questo comando esattamente come se si è incluso tutti hello singoli parametri della riga di comando hello:</span><span class="sxs-lookup"><span data-stu-id="4483b-270">AzCopy processes this command just as it would if you included all of hello individual parameters on hello command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="4483b-271">Specificare una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="4483b-271">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="4483b-272">È inoltre possibile specificare una firma di accesso condiviso nel contenitore hello URI:</span><span class="sxs-lookup"><span data-stu-id="4483b-272">You can also specify a SAS on hello container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="4483b-273">Cartella del file journal</span><span class="sxs-lookup"><span data-stu-id="4483b-273">Journal file folder</span></span>
<span data-ttu-id="4483b-274">Ogni volta che si esegue un comando tooAzCopy, controlla se è presente un file journal nella cartella predefinita hello o se esiste in una cartella specificata tramite questa opzione.</span><span class="sxs-lookup"><span data-stu-id="4483b-274">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="4483b-275">Se non esiste alcun file journal hello in entrambe le posizioni, AzCopy considera nuova operazione hello e genera un nuovo file journal.</span><span class="sxs-lookup"><span data-stu-id="4483b-275">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="4483b-276">Se esistono file journal hello, AzCopy controllerà se riga di comando hello immesso corrisponde a riga di comando hello in file journal hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-276">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="4483b-277">Se due righe di comando hello corrispondono, AzCopy riprende hello incompleti.</span><span class="sxs-lookup"><span data-stu-id="4483b-277">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="4483b-278">Se non corrispondono, si tooeither richiesta sovrascrittura hello journal file toostart una nuova operazione o toocancel hello operazione corrente.</span><span class="sxs-lookup"><span data-stu-id="4483b-278">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="4483b-279">Se si desidera toouse hello percorso predefinito file journal hello:</span><span class="sxs-lookup"><span data-stu-id="4483b-279">If you want toouse hello default location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="4483b-280">Se si omette l'opzione `/Z`, oppure specificare l'opzione `/Z` senza percorso della cartella hello, come illustrato in precedenza, AzCopy crea file journal hello nel percorso predefinito di hello, ovvero `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="4483b-280">If you omit option `/Z`, or specify option `/Z` without hello folder path, as shown above, AzCopy creates hello journal file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="4483b-281">Se il file journal di hello esiste già, quindi AzCopy riprende l'operazione di hello basato su file journal hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-281">If hello journal file already exists, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="4483b-282">Se si desidera toospecify un percorso personalizzato per il file journal hello:</span><span class="sxs-lookup"><span data-stu-id="4483b-282">If you want toospecify a custom location for hello journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="4483b-283">Questo esempio crea file journal hello se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="4483b-283">This example creates hello journal file if it does not already exist.</span></span> <span data-ttu-id="4483b-284">Se esiste, quindi AzCopy riprende l'operazione di hello basato su file journal hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-284">If it does exist, then AzCopy resumes hello operation based on hello journal file.</span></span>

<span data-ttu-id="4483b-285">Se si desidera tooresume un'operazione di AzCopy:</span><span class="sxs-lookup"><span data-stu-id="4483b-285">If you want tooresume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="4483b-286">In questo esempio riprende hello ultima operazione, che potrebbe non essere stata toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4483b-286">This example resumes hello last operation, which may have failed toocomplete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="4483b-287">Generare un file di log</span><span class="sxs-lookup"><span data-stu-id="4483b-287">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="4483b-288">Se si specifica l'opzione `/V` senza fornire un log dettagliato di percorso toohello file, quindi AzCopy crea hello file di log nel percorso predefinito di hello, ovvero `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="4483b-288">If you specify option `/V` without providing a file path toohello verbose log, then AzCopy creates hello log file in hello default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="4483b-289">In caso contrario, è possibile creare un file di log in un percorso personalizzato:</span><span class="sxs-lookup"><span data-stu-id="4483b-289">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="4483b-290">Si noti che se si specifica un percorso relativo seguente opzione `/V`, ad esempio `/V:test/azcopy1.log`, log dettagliato hello viene creato nella directory di lavoro corrente di hello all'interno di una sottocartella denominata `test`.</span><span class="sxs-lookup"><span data-stu-id="4483b-290">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then hello verbose log is created in hello current working directory within a subfolder named `test`.</span></span>

### <a name="specify-hello-number-of-concurrent-operations-toostart"></a><span data-ttu-id="4483b-291">Specificare il numero di hello di operazioni simultanee toostart</span><span class="sxs-lookup"><span data-stu-id="4483b-291">Specify hello number of concurrent operations toostart</span></span>
<span data-ttu-id="4483b-292">Opzione `/NC` specifica hello numero di operazioni di copia simultanea.</span><span class="sxs-lookup"><span data-stu-id="4483b-292">Option `/NC` specifies hello number of concurrent copy operations.</span></span> <span data-ttu-id="4483b-293">Per impostazione predefinita, AzCopy inizia un certo numero di velocità effettiva di trasferimento dei dati di operazioni simultanee tooincrease hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-293">By default, AzCopy starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="4483b-294">Per le operazioni di tabella, il numero di hello di operazioni simultanee è uguale toohello numero di processori che disponibili.</span><span class="sxs-lookup"><span data-stu-id="4483b-294">For Table operations, hello number of concurrent operations is equal toohello number of processors you have.</span></span> <span data-ttu-id="4483b-295">Per operazioni di Blob e File, il numero di hello di operazioni simultanee è uguale a numero hello 8 volte di processori che disponibili.</span><span class="sxs-lookup"><span data-stu-id="4483b-295">For Blob and File operations, hello number of concurrent operations is equal 8 times hello number of processors you have.</span></span> <span data-ttu-id="4483b-296">Se si esegue AzCopy attraverso una rete con larghezza di banda ridotta, è possibile specificare un numero inferiore per /NC tooavoid errore di concorrenza di risorse.</span><span class="sxs-lookup"><span data-stu-id="4483b-296">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC tooavoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="4483b-297">Eseguire AzCopy nell'Emulatore di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4483b-297">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="4483b-298">È possibile eseguire AzCopy hello [emulatore di archiviazione Azure](storage-use-emulator.md) per i BLOB:</span><span class="sxs-lookup"><span data-stu-id="4483b-298">You can run AzCopy against hello [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="4483b-299">e le tabelle:</span><span class="sxs-lookup"><span data-stu-id="4483b-299">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="4483b-300">Parametri di AzCopy</span><span class="sxs-lookup"><span data-stu-id="4483b-300">AzCopy Parameters</span></span>
<span data-ttu-id="4483b-301">I parametri per AzCopy sono descritti nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="4483b-301">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="4483b-302">È anche possibile digitare uno dei seguenti comandi dalla riga di comando hello per informazioni sull'utilizzo di AzCopy hello:</span><span class="sxs-lookup"><span data-stu-id="4483b-302">You can also type one of hello following commands from hello command line for help in using AzCopy:</span></span>

* <span data-ttu-id="4483b-303">Per assistenza dettagliata della riga di comando per AzCopy: `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="4483b-303">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="4483b-304">Per assistenza dettagliata con un parametro di AzCopy: `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="4483b-304">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="4483b-305">Per esempi della riga di comando: `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="4483b-305">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="4483b-306">/Source: "source"</span><span class="sxs-lookup"><span data-stu-id="4483b-306">/Source:"source"</span></span>
<span data-ttu-id="4483b-307">Specifica i dati di origine hello da cui toocopy.</span><span class="sxs-lookup"><span data-stu-id="4483b-307">Specifies hello source data from which toocopy.</span></span> <span data-ttu-id="4483b-308">Hello origine può essere una directory del file system, un contenitore blob, una directory virtuale di blob, una condivisione di file di archiviazione, una directory di archiviazione di file o una tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="4483b-308">hello source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="4483b-309">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-309">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="4483b-310">/Dest:"destination"</span><span class="sxs-lookup"><span data-stu-id="4483b-310">/Dest:"destination"</span></span>
<span data-ttu-id="4483b-311">Specifica hello destinazione toocopy per.</span><span class="sxs-lookup"><span data-stu-id="4483b-311">Specifies hello destination toocopy to.</span></span> <span data-ttu-id="4483b-312">Hello destinazione può essere una directory del file system, un contenitore blob, una directory virtuale di blob, una condivisione di file di archiviazione, una directory di archiviazione di file o una tabella di Azure.</span><span class="sxs-lookup"><span data-stu-id="4483b-312">hello destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="4483b-313">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-313">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="4483b-314">/Pattern:"file-pattern"</span><span class="sxs-lookup"><span data-stu-id="4483b-314">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="4483b-315">Specifica uno schema di file che indica quale toocopy file.</span><span class="sxs-lookup"><span data-stu-id="4483b-315">Specifies a file pattern that indicates which files toocopy.</span></span> <span data-ttu-id="4483b-316">comportamento di Hello del parametro /Pattern hello è determinato dal percorso hello hello dei dati di origine e la presenza di hello di opzione della modalità ricorsiva hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-316">hello behavior of hello /Pattern parameter is determined by hello location of hello source data, and hello presence of hello recursive mode option.</span></span> <span data-ttu-id="4483b-317">È possibile specificare la modalità ricorsiva tramite l'opzione /S.</span><span class="sxs-lookup"><span data-stu-id="4483b-317">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="4483b-318">Se l'origine specificata hello è una directory nel file system di hello, caratteri jolly standard vengono in effetti, e quindi il modello di file hello fornito viene confrontato con i file nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-318">If hello specified source is a directory in hello file system, then standard wildcards are in effect, and hello file pattern provided is matched against files within hello directory.</span></span> <span data-ttu-id="4483b-319">Se l'opzione che /s è specificata, quindi AzCopy corrisponde anche modello specificato di hello in tutti i file nelle sottocartelle nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-319">If option /S is specified, then AzCopy also matches hello specified pattern against all files in any subfolders beneath hello directory.</span></span>

<span data-ttu-id="4483b-320">Se l'origine specificata hello è un contenitore blob o directory virtuale, i caratteri jolly non vengono applicate.</span><span class="sxs-lookup"><span data-stu-id="4483b-320">If hello specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="4483b-321">Se l'opzione che /s è specificata, quindi AzCopy interpreta il criterio di file specificato hello come prefisso blob.</span><span class="sxs-lookup"><span data-stu-id="4483b-321">If option /S is specified, then AzCopy interprets hello specified file pattern as a blob prefix.</span></span> <span data-ttu-id="4483b-322">Se opzione che /s non viene specificato, quindi AzCopy corrisponde allo schema di file di hello e i nomi dei blob esatto.</span><span class="sxs-lookup"><span data-stu-id="4483b-322">If option /S is not specified, then AzCopy matches hello file pattern against exact blob names.</span></span>

<span data-ttu-id="4483b-323">Se hello specificato origine è una condivisione di file di Azure, è necessario specificare hello nome esatto del file, (ad esempio, ABC) toocopy un singolo file, oppure specificare opzione /S toocopy tutti i file in modo ricorsivo condivisione hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-323">If hello specified source is an Azure file share, then you must either specify hello exact file name, (e.g. abc.txt) toocopy a single file, or specify option /S toocopy all files in hello share recursively.</span></span> <span data-ttu-id="4483b-324">Il tentativo toospecify un modello di file e l'opzione /S insieme genererà un errore.</span><span class="sxs-lookup"><span data-stu-id="4483b-324">Attempting toospecify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="4483b-325">AzCopy Usa la corrispondenza tra maiuscole e minuscole quando hello /Source è un contenitore blob o directory virtuale di blob e utilizza distinzione corrispondenti in tutti gli altri casi di hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-325">AzCopy uses case-sensitive matching when hello /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all hello other cases.</span></span>

<span data-ttu-id="4483b-326">Hello file criterio predefinito utilizzato quando non è specificato alcun modello di file è *.*</span><span class="sxs-lookup"><span data-stu-id="4483b-326">hello default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="4483b-327">per un percorso del file system o un prefisso vuoto per un percorso di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4483b-327">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="4483b-328">Non è consentito specificare più criteri file.</span><span class="sxs-lookup"><span data-stu-id="4483b-328">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="4483b-329">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="4483b-329">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="4483b-330">/DestKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="4483b-330">/DestKey:"storage-key"</span></span>
<span data-ttu-id="4483b-331">Specifica una chiave dell'account di archiviazione per la risorsa di destinazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-331">Specifies hello storage account key for hello destination resource.</span></span>

<span data-ttu-id="4483b-332">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-332">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="4483b-333">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="4483b-333">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="4483b-334">Specifica una firma di accesso condiviso (SAS) con autorizzazioni di lettura e scrittura per la destinazione di hello (se applicabile).</span><span class="sxs-lookup"><span data-stu-id="4483b-334">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for hello destination (if applicable).</span></span> <span data-ttu-id="4483b-335">Consente di racchiudere hello SAS tra virgolette doppie, in quanto potrebbe contiene i caratteri speciali della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="4483b-335">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="4483b-336">Se risorsa di destinazione hello è un contenitore blob, condivisione file o una tabella, è possibile specificare questa opzione, seguita dal token di firma di accesso condiviso hello oppure è possibile specificare hello firma di accesso condiviso come parte del contenitore blob di destinazione hello, condivisione file o l'URI della tabella, senza questa opzione.</span><span class="sxs-lookup"><span data-stu-id="4483b-336">If hello destination resource is a blob container, file share or table, you can either specify this option followed by hello SAS token, or you can specify hello SAS as part of hello destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="4483b-337">Se hello origine e destinazione siano entrambi i BLOB, quindi il blob di destinazione hello deve risiedere all'interno di hello stesso account di archiviazione blob di origine hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-337">If hello source and destination are both blobs, then hello destination blob must reside within hello same storage account as hello source blob.</span></span>

<span data-ttu-id="4483b-338">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-338">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="4483b-339">/SourceKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="4483b-339">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="4483b-340">Specifica una chiave dell'account di archiviazione per la risorsa di origine hello hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-340">Specifies hello storage account key for hello source resource.</span></span>

<span data-ttu-id="4483b-341">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="4483b-342">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="4483b-342">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="4483b-343">Specifica una firma di accesso condiviso con le autorizzazioni di lettura ed elenco per hello origine (se applicabile).</span><span class="sxs-lookup"><span data-stu-id="4483b-343">Specifies a Shared Access Signature with READ and LIST permissions for hello source (if applicable).</span></span> <span data-ttu-id="4483b-344">Consente di racchiudere hello SAS tra virgolette doppie, in quanto potrebbe contiene i caratteri speciali della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="4483b-344">Surround hello SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="4483b-345">Se hello origine risorsa è un contenitore di blob e viene fornita una chiave né una firma di accesso condiviso, il contenitore di blob hello verrà letta tramite l'accesso anonimo.</span><span class="sxs-lookup"><span data-stu-id="4483b-345">If hello source resource is a blob container, and neither a key nor a SAS is provided, then hello blob container will be read via anonymous access.</span></span>

<span data-ttu-id="4483b-346">Se l'origine di hello è una condivisione file o una tabella, è necessario specificare una chiave o una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="4483b-346">If hello source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="4483b-347">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-347">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="4483b-348">/S</span><span class="sxs-lookup"><span data-stu-id="4483b-348">/S</span></span>
<span data-ttu-id="4483b-349">Specifica la modalità ricorsiva per le operazioni di copia.</span><span class="sxs-lookup"><span data-stu-id="4483b-349">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="4483b-350">In modalità ricorsiva, AzCopy verranno copiati tutti i BLOB o i file che corrispondono a hello criterio di file specificato, inclusi quelli nelle sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="4483b-350">In recursive mode, AzCopy will copy all blobs or files that match hello specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="4483b-351">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="4483b-351">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="4483b-352">/BlobType:"block" | "page" | "append"</span><span class="sxs-lookup"><span data-stu-id="4483b-352">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="4483b-353">Specifica se il blob di destinazione hello è un blob in blocchi, un blob di pagine o un blob di aggiunta.</span><span class="sxs-lookup"><span data-stu-id="4483b-353">Specifies whether hello destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="4483b-354">Questa opzione è applicabile solo per l'upload di un BLOB.</span><span class="sxs-lookup"><span data-stu-id="4483b-354">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="4483b-355">In caso contrario, viene generato un errore.</span><span class="sxs-lookup"><span data-stu-id="4483b-355">Otherwise, an error is generated.</span></span> <span data-ttu-id="4483b-356">Se la destinazione hello è un blob e questa opzione non è specificata, per impostazione predefinita, AzCopy crea un blob in blocchi.</span><span class="sxs-lookup"><span data-stu-id="4483b-356">If hello destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="4483b-357">**Applicabile a:** BLOB</span><span class="sxs-lookup"><span data-stu-id="4483b-357">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="4483b-358">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="4483b-358">/CheckMD5</span></span>
<span data-ttu-id="4483b-359">Calcola un hash MD5 per i dati scaricati e verifica che l'hash MD5 hello archiviati nel blob hello o hash calcolato hello corrisponde a proprietà Content-MD5 del file.</span><span class="sxs-lookup"><span data-stu-id="4483b-359">Calculates an MD5 hash for downloaded data and verifies that hello MD5 hash stored in hello blob or file's Content-MD5 property matches hello calculated hash.</span></span> <span data-ttu-id="4483b-360">controllo Hello MD5 è disattivata per impostazione predefinita, pertanto è necessario specificare questo controllo di MD5 hello tooperform opzione quando il download dei dati.</span><span class="sxs-lookup"><span data-stu-id="4483b-360">hello MD5 check is turned off by default, so you must specify this option tooperform hello MD5 check when downloading data.</span></span>

<span data-ttu-id="4483b-361">Si noti che di archiviazione di Azure non garantisce che hello hash MD5 archiviato per il blob hello o file sia aggiornato.</span><span class="sxs-lookup"><span data-stu-id="4483b-361">Note that Azure Storage doesn't guarantee that hello MD5 hash stored for hello blob or file is up-to-date.</span></span> <span data-ttu-id="4483b-362">È hello tooupdate di responsabilità del client MD5 ogni volta che viene modificato hello blob o file.</span><span class="sxs-lookup"><span data-stu-id="4483b-362">It is client's responsibility tooupdate hello MD5 whenever hello blob or file is modified.</span></span>

<span data-ttu-id="4483b-363">AzCopy sempre impostata hello Content-MD5 per un blob di Azure o il file dopo averlo caricato toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="4483b-363">AzCopy always sets hello Content-MD5 property for an Azure blob or file after uploading it toohello service.</span></span>  

<span data-ttu-id="4483b-364">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="4483b-364">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="4483b-365">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="4483b-365">/Snapshot</span></span>
<span data-ttu-id="4483b-366">Indica se gli snapshot tootransfer.</span><span class="sxs-lookup"><span data-stu-id="4483b-366">Indicates whether tootransfer snapshots.</span></span> <span data-ttu-id="4483b-367">Questa opzione è valida solo quando l'origine hello è un blob.</span><span class="sxs-lookup"><span data-stu-id="4483b-367">This option is only valid when hello source is a blob.</span></span>

<span data-ttu-id="4483b-368">Hello snapshot blob trasferiti vengono rinominati in questo formato:. Extension blob-name (ora dello snapshot)</span><span class="sxs-lookup"><span data-stu-id="4483b-368">hello transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="4483b-369">Per impostazione predefinita, gli snapshot non vengono copiati.</span><span class="sxs-lookup"><span data-stu-id="4483b-369">By default, snapshots are not copied.</span></span>

<span data-ttu-id="4483b-370">**Applicabile a:** BLOB</span><span class="sxs-lookup"><span data-stu-id="4483b-370">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="4483b-371">/V:[verbose-log-file]</span><span class="sxs-lookup"><span data-stu-id="4483b-371">/V:[verbose-log-file]</span></span>
<span data-ttu-id="4483b-372">Esegue l'output dei messaggi di stato dettagliati in un file di log.</span><span class="sxs-lookup"><span data-stu-id="4483b-372">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="4483b-373">Per impostazione predefinita, il file di log dettagliato hello denominato AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="4483b-373">By default, hello verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="4483b-374">Se si specifica un percorso del file esistente per questa opzione, log dettagliato hello sarà toothat aggiunto file.</span><span class="sxs-lookup"><span data-stu-id="4483b-374">If you specify an existing file location for this option, hello verbose log will be appended toothat file.</span></span>  

<span data-ttu-id="4483b-375">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-375">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="4483b-376">/Z:[journal-file-folder]</span><span class="sxs-lookup"><span data-stu-id="4483b-376">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="4483b-377">Specifica la cartella del file journal per la ripresa di un'operazione.</span><span class="sxs-lookup"><span data-stu-id="4483b-377">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="4483b-378">AzCopy supporta sempre la ripresa di un'operazione interrotta.</span><span class="sxs-lookup"><span data-stu-id="4483b-378">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="4483b-379">Se questa opzione non è specificata o viene specificato senza un percorso di cartella, AzCopy crea nel percorso predefinito di hello, ovvero % LocalAppData%\Microsoft\Azure\AzCopy file journal hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-379">If this option is not specified, or it is specified without a folder path, then AzCopy will create hello journal file in hello default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="4483b-380">Ogni volta che si esegue un comando tooAzCopy, controlla se è presente un file journal nella cartella predefinita hello o se esiste in una cartella specificata tramite questa opzione.</span><span class="sxs-lookup"><span data-stu-id="4483b-380">Each time you issue a command tooAzCopy, it checks whether a journal file exists in hello default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="4483b-381">Se non esiste alcun file journal hello in entrambe le posizioni, AzCopy considera nuova operazione hello e genera un nuovo file journal.</span><span class="sxs-lookup"><span data-stu-id="4483b-381">If hello journal file does not exist in either place, AzCopy treats hello operation as new and generates a new journal file.</span></span>

<span data-ttu-id="4483b-382">Se esistono file journal hello, AzCopy controllerà se riga di comando hello immesso corrisponde a riga di comando hello in file journal hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-382">If hello journal file does exist, AzCopy will check whether hello command line that you input matches hello command line in hello journal file.</span></span> <span data-ttu-id="4483b-383">Se due righe di comando hello corrispondono, AzCopy riprende hello incompleti.</span><span class="sxs-lookup"><span data-stu-id="4483b-383">If hello two command lines match, AzCopy resumes hello incomplete operation.</span></span> <span data-ttu-id="4483b-384">Se non corrispondono, si tooeither richiesta sovrascrittura hello journal file toostart una nuova operazione o toocancel hello operazione corrente.</span><span class="sxs-lookup"><span data-stu-id="4483b-384">If they do not match, you will be prompted tooeither overwrite hello journal file toostart a new operation, or toocancel hello current operation.</span></span>

<span data-ttu-id="4483b-385">file journal Hello viene eliminato dopo il completamento dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-385">hello journal file is deleted upon successful completion of hello operation.</span></span>

<span data-ttu-id="4483b-386">Si noti che la ripresa di un'operazione da un file journal creato da una versione precedente di AzCopy non è supportata.</span><span class="sxs-lookup"><span data-stu-id="4483b-386">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="4483b-387">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-387">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="4483b-388">/@:"parameter-file"</span><span class="sxs-lookup"><span data-stu-id="4483b-388">/@:"parameter-file"</span></span>
<span data-ttu-id="4483b-389">Specifica un file contenente parametri.</span><span class="sxs-lookup"><span data-stu-id="4483b-389">Specifies a file that contains parameters.</span></span> <span data-ttu-id="4483b-390">I processi di AzCopy hello parametri nel file hello come se fossero stati specificati nella riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-390">AzCopy processes hello parameters in hello file just as if they had been specified on hello command line.</span></span>

<span data-ttu-id="4483b-391">In un file di risposta è possibile specificare più parametri su una sola riga o specificare un parametro su ogni riga.</span><span class="sxs-lookup"><span data-stu-id="4483b-391">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="4483b-392">Si noti che un singolo parametro non può estendersi su più righe.</span><span class="sxs-lookup"><span data-stu-id="4483b-392">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="4483b-393">File di risposta possono includere righe di commenti che iniziano con il simbolo # hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-393">Response files can include comments lines that begin with hello # symbol.</span></span>

<span data-ttu-id="4483b-394">È possibile specificare più file di risposta.</span><span class="sxs-lookup"><span data-stu-id="4483b-394">You can specify multiple response files.</span></span> <span data-ttu-id="4483b-395">Tuttavia, tenere presente che AzCopy non supporta file di risposta annidati.</span><span class="sxs-lookup"><span data-stu-id="4483b-395">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="4483b-396">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-396">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="4483b-397">/Y</span><span class="sxs-lookup"><span data-stu-id="4483b-397">/Y</span></span>
<span data-ttu-id="4483b-398">Elimina tutte le richieste di conferma di AzCopy.</span><span class="sxs-lookup"><span data-stu-id="4483b-398">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="4483b-399">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="4483b-400">/L</span><span class="sxs-lookup"><span data-stu-id="4483b-400">/L</span></span>
<span data-ttu-id="4483b-401">Specifica solo un'operazione di elenco, non viene copiato alcun dato.</span><span class="sxs-lookup"><span data-stu-id="4483b-401">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="4483b-402">AzCopy interpreterà hello utilizzo di questa opzione come una simulazione per riga di comando hello in esecuzione senza questa opzione /L e contare il numero di oggetti verrà copiato, è possibile specificare l'opzione /V in hello stesso tempo toocheck gli oggetti che verranno copiati nel log dettagliato hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-402">AzCopy will interpret hello using of this option as a simulation for running hello command line without this option /L and count how many objects will be copied, you can specify option /V at hello same time toocheck which objects will be copied in hello verbose log.</span></span>

<span data-ttu-id="4483b-403">comportamento di Hello di questa opzione è inoltre determinato dalla posizione hello hello dei dati di origine e la presenza di hello di hello ricorsiva modalità /S e file di modello opzione /Pattern.</span><span class="sxs-lookup"><span data-stu-id="4483b-403">hello behavior of this option is also determined by hello location of hello source data and hello presence of hello recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="4483b-404">AzCopy richiede l'autorizzazione ELENCO e LETTURA per questo percorso di origine quando si utilizza questa opzione.</span><span class="sxs-lookup"><span data-stu-id="4483b-404">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="4483b-405">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="4483b-405">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="4483b-406">/MT</span><span class="sxs-lookup"><span data-stu-id="4483b-406">/MT</span></span>
<span data-ttu-id="4483b-407">Imposta l'ora dell'ultima modifica del file scaricato hello toobe hello stesso come blob di origine hello o del file.</span><span class="sxs-lookup"><span data-stu-id="4483b-407">Sets hello downloaded file's last-modified time toobe hello same as hello source blob or file's.</span></span>

<span data-ttu-id="4483b-408">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="4483b-408">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="4483b-409">/XN</span><span class="sxs-lookup"><span data-stu-id="4483b-409">/XN</span></span>
<span data-ttu-id="4483b-410">Esclude una risorsa di origine più recente.</span><span class="sxs-lookup"><span data-stu-id="4483b-410">Excludes a newer source resource.</span></span> <span data-ttu-id="4483b-411">risorsa Hello non verrà copiato se l'ora dell'ultima modifica dell'origine hello hello è hello uguale o più recente di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4483b-411">hello resource will not be copied if hello last modified time of hello source is hello same or newer than destination.</span></span>

<span data-ttu-id="4483b-412">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="4483b-412">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="4483b-413">/XO</span><span class="sxs-lookup"><span data-stu-id="4483b-413">/XO</span></span>
<span data-ttu-id="4483b-414">Esclude una risorsa di origine meno recente.</span><span class="sxs-lookup"><span data-stu-id="4483b-414">Excludes an older source resource.</span></span> <span data-ttu-id="4483b-415">risorsa Hello non verrà copiato se l'ora dell'ultima modifica dell'origine hello hello è hello uguale o più vecchi di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4483b-415">hello resource will not be copied if hello last modified time of hello source is hello same or older than destination.</span></span>

<span data-ttu-id="4483b-416">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="4483b-416">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="4483b-417">/A</span><span class="sxs-lookup"><span data-stu-id="4483b-417">/A</span></span>
<span data-ttu-id="4483b-418">Carica solo i file che è sono impostato l'attributo Archive hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-418">Uploads only files that have hello Archive attribute set.</span></span>

<span data-ttu-id="4483b-419">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="4483b-419">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="4483b-420">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="4483b-420">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="4483b-421">Caricamenti solo i file che dispongono di alcuna hello specificare set di attributi.</span><span class="sxs-lookup"><span data-stu-id="4483b-421">Uploads only files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="4483b-422">Gli attributi disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="4483b-422">Available attributes include:</span></span>

* <span data-ttu-id="4483b-423">R = File di sola lettura</span><span class="sxs-lookup"><span data-stu-id="4483b-423">R = Read-only files</span></span>
* <span data-ttu-id="4483b-424">A = File pronti per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="4483b-424">A = Files ready for archiving</span></span>
* <span data-ttu-id="4483b-425">S = File di sistema</span><span class="sxs-lookup"><span data-stu-id="4483b-425">S = System files</span></span>
* <span data-ttu-id="4483b-426">H = File nascosti</span><span class="sxs-lookup"><span data-stu-id="4483b-426">H = Hidden files</span></span>
* <span data-ttu-id="4483b-427">C = File compressi</span><span class="sxs-lookup"><span data-stu-id="4483b-427">C = Compressed files</span></span>
* <span data-ttu-id="4483b-428">N = File normali</span><span class="sxs-lookup"><span data-stu-id="4483b-428">N = Normal files</span></span>
* <span data-ttu-id="4483b-429">E = File crittografati</span><span class="sxs-lookup"><span data-stu-id="4483b-429">E = Encrypted files</span></span>
* <span data-ttu-id="4483b-430">T = File temporanei</span><span class="sxs-lookup"><span data-stu-id="4483b-430">T = Temporary files</span></span>
* <span data-ttu-id="4483b-431">O = File offline</span><span class="sxs-lookup"><span data-stu-id="4483b-431">O = Offline files</span></span>
* <span data-ttu-id="4483b-432">I = File non indicizzati</span><span class="sxs-lookup"><span data-stu-id="4483b-432">I = Non-indexed files</span></span>

<span data-ttu-id="4483b-433">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="4483b-433">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="4483b-434">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="4483b-434">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="4483b-435">Esclude i file contenenti hello specificato set di attributi.</span><span class="sxs-lookup"><span data-stu-id="4483b-435">Excludes files that have any of hello specified attributes set.</span></span>

<span data-ttu-id="4483b-436">Gli attributi disponibili sono:</span><span class="sxs-lookup"><span data-stu-id="4483b-436">Available attributes include:</span></span>

* <span data-ttu-id="4483b-437">R = File di sola lettura</span><span class="sxs-lookup"><span data-stu-id="4483b-437">R = Read-only files</span></span>
* <span data-ttu-id="4483b-438">A = File pronti per l'archiviazione</span><span class="sxs-lookup"><span data-stu-id="4483b-438">A = Files ready for archiving</span></span>
* <span data-ttu-id="4483b-439">S = File di sistema</span><span class="sxs-lookup"><span data-stu-id="4483b-439">S = System files</span></span>
* <span data-ttu-id="4483b-440">H = File nascosti</span><span class="sxs-lookup"><span data-stu-id="4483b-440">H = Hidden files</span></span>
* <span data-ttu-id="4483b-441">C = File compressi</span><span class="sxs-lookup"><span data-stu-id="4483b-441">C = Compressed files</span></span>
* <span data-ttu-id="4483b-442">N = File normali</span><span class="sxs-lookup"><span data-stu-id="4483b-442">N = Normal files</span></span>
* <span data-ttu-id="4483b-443">E = File crittografati</span><span class="sxs-lookup"><span data-stu-id="4483b-443">E = Encrypted files</span></span>
* <span data-ttu-id="4483b-444">T = File temporanei</span><span class="sxs-lookup"><span data-stu-id="4483b-444">T = Temporary files</span></span>
* <span data-ttu-id="4483b-445">O = File offline</span><span class="sxs-lookup"><span data-stu-id="4483b-445">O = Offline files</span></span>
* <span data-ttu-id="4483b-446">I = File non indicizzati</span><span class="sxs-lookup"><span data-stu-id="4483b-446">I = Non-indexed files</span></span>

<span data-ttu-id="4483b-447">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="4483b-447">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="4483b-448">/Delimiter:"delimiter"</span><span class="sxs-lookup"><span data-stu-id="4483b-448">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="4483b-449">Indica il carattere delimitatore di hello utilizzato toodelimit le directory virtuali in un nome di blob.</span><span class="sxs-lookup"><span data-stu-id="4483b-449">Indicates hello delimiter character used toodelimit virtual directories in a blob name.</span></span>

<span data-ttu-id="4483b-450">Per impostazione predefinita, viene utilizzato AzCopy / come carattere di delimitazione hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-450">By default, AzCopy uses / as hello delimiter character.</span></span> <span data-ttu-id="4483b-451">Tuttavia, a questo scopo supporta anche l'uso di caratteri comuni, ad esempio @, # o %.</span><span class="sxs-lookup"><span data-stu-id="4483b-451">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="4483b-452">Se è necessario tooinclude uno di questi caratteri speciali nella riga di comando hello, racchiudere il nome file hello tra virgolette doppie.</span><span class="sxs-lookup"><span data-stu-id="4483b-452">If you need tooinclude one of these special characters on hello command line, enclose hello file name with double quotes.</span></span>

<span data-ttu-id="4483b-453">Questa opzione si applica solo per il download di BLOB.</span><span class="sxs-lookup"><span data-stu-id="4483b-453">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="4483b-454">**Applicabile a:** BLOB</span><span class="sxs-lookup"><span data-stu-id="4483b-454">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="4483b-455">/NC:"number-of-concurrent-operations"</span><span class="sxs-lookup"><span data-stu-id="4483b-455">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="4483b-456">Specifica il numero di hello di operazioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="4483b-456">Specifies hello number of concurrent operations.</span></span>

<span data-ttu-id="4483b-457">AzCopy per impostazione predefinita viene avviato un determinato numero di velocità effettiva di trasferimento dei dati di operazioni simultanee tooincrease hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-457">AzCopy by default starts a certain number of concurrent operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="4483b-458">Si noti che un numero elevato di operazioni simultanee in un ambiente di larghezza di banda bassa può sovraccaricare la connessione di rete hello e impedire completamente il completamento delle operazioni hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-458">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm hello network connection and prevent hello operations from fully completing.</span></span> <span data-ttu-id="4483b-459">Limitare le operazioni simultanee in base alla larghezza di banda di rete effettivamente disponibile.</span><span class="sxs-lookup"><span data-stu-id="4483b-459">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="4483b-460">limite massimo di Hello per le operazioni simultanee è 512.</span><span class="sxs-lookup"><span data-stu-id="4483b-460">hello upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="4483b-461">**Applicabile a:** BLOB, file, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-461">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="4483b-462">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="4483b-462">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="4483b-463">Specifica che hello `source` risorsa è un blob disponibile nell'ambiente di sviluppo locale hello, in esecuzione nell'emulatore di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-463">Specifies that hello `source` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="4483b-464">**Applicabile a:** BLOB, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-464">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="4483b-465">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="4483b-465">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="4483b-466">Specifica che hello `destination` risorsa è un blob disponibile nell'ambiente di sviluppo locale hello, in esecuzione nell'emulatore di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-466">Specifies that hello `destination` resource is a blob available in hello local development environment, running in hello storage emulator.</span></span>

<span data-ttu-id="4483b-467">**Applicabile a:** BLOB, tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="4483b-468">/PKRS:"key1#key2#key3#..."</span><span class="sxs-lookup"><span data-stu-id="4483b-468">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="4483b-469">Divisioni hello tooenable di intervalli di chiavi di partizione esportazione dei dati in parallelo, il che aumenta la velocità di hello dell'operazione di esportazione hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-469">Splits hello partition key range tooenable exporting table data in parallel, which increases hello speed of hello export operation.</span></span>

<span data-ttu-id="4483b-470">Se questa opzione non è specificata, AzCopy utilizza entità della tabella tooexport un singolo thread.</span><span class="sxs-lookup"><span data-stu-id="4483b-470">If this option is not specified, then AzCopy uses a single thread tooexport table entities.</span></span> <span data-ttu-id="4483b-471">Ad esempio, se hello utente specifica /PKRS: "#bb aa", quindi AzCopy avvia tre operazioni simultanee.</span><span class="sxs-lookup"><span data-stu-id="4483b-471">For example, if hello user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="4483b-472">Ogni operazione esporta uno dei tre intervalli di chiavi di partizione, nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="4483b-472">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="4483b-473">[first-partition-key, aa)</span><span class="sxs-lookup"><span data-stu-id="4483b-473">[first-partition-key, aa)</span></span>

  <span data-ttu-id="4483b-474">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="4483b-474">[aa, bb)</span></span>

  <span data-ttu-id="4483b-475">[bb, last-partition-key]</span><span class="sxs-lookup"><span data-stu-id="4483b-475">[bb, last-partition-key]</span></span>

<span data-ttu-id="4483b-476">**Applicabile a:** tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-476">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="4483b-477">/SplitSize:"file-size"</span><span class="sxs-lookup"><span data-stu-id="4483b-477">/SplitSize:"file-size"</span></span>
<span data-ttu-id="4483b-478">Specifica hello esportato dividere dimensioni in MB, hello di valore minimo consentito è 32.</span><span class="sxs-lookup"><span data-stu-id="4483b-478">Specifies hello exported file split size in MB, hello minimal value allowed is 32.</span></span>

<span data-ttu-id="4483b-479">Se questa opzione non è specificata, AzCopy esporterà toosingle file di dati di tabella.</span><span class="sxs-lookup"><span data-stu-id="4483b-479">If this option is not specified, AzCopy will export table data toosingle file.</span></span>

<span data-ttu-id="4483b-480">Se i dati di tabella hello esportata tooa blob, e hello esportato il file raggiunge il limite di 200 GB hello per le dimensioni del blob, AzCopy suddividerà hello file esportato, anche se questa opzione non è specificata.</span><span class="sxs-lookup"><span data-stu-id="4483b-480">If hello table data is exported tooa blob, and hello exported file size reaches hello 200 GB limit for blob size, then AzCopy will split hello exported file, even if this option is not specified.</span></span>

<span data-ttu-id="4483b-481">**Applicabile a:** tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-481">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="4483b-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="4483b-482">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="4483b-483">Specifica il comportamento di importazione hello tabella dati.</span><span class="sxs-lookup"><span data-stu-id="4483b-483">Specifies hello table data import behavior.</span></span>

* <span data-ttu-id="4483b-484">InsertOrSkip - Ignora un'entità esistente o inserisce una nuova entità se non esiste nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-484">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="4483b-485">InsertOrMerge - unisce un'entità esistente o inserisce una nuova entità se non esiste nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-485">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in hello table.</span></span>
* <span data-ttu-id="4483b-486">InsertOrReplace - sostituisce un'entità esistente o inserisce una nuova entità se non esiste nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-486">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in hello table.</span></span>

<span data-ttu-id="4483b-487">**Applicabile a:** tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-487">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="4483b-488">/Manifest:"manifest-file"</span><span class="sxs-lookup"><span data-stu-id="4483b-488">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="4483b-489">Specifica il file manifesto hello per tabella hello esportazione e importazione di operazione.</span><span class="sxs-lookup"><span data-stu-id="4483b-489">Specifies hello manifest file for hello table export and import operation.</span></span>

<span data-ttu-id="4483b-490">Questa opzione è facoltativa durante l'operazione di esportazione hello, AzCopy genererà un file manifesto con il nome predefinito se non si specifica questa opzione.</span><span class="sxs-lookup"><span data-stu-id="4483b-490">This option is optional during hello export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="4483b-491">Questa opzione è necessaria durante l'operazione di importazione hello per individuare i file di dati hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-491">This option is required during hello import operation for locating hello data files.</span></span>

<span data-ttu-id="4483b-492">**Applicabile a:** tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-492">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="4483b-493">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="4483b-493">/SyncCopy</span></span>
<span data-ttu-id="4483b-494">Indica se toosynchronously copiare BLOB o i file tra due endpoint di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4483b-494">Indicates whether toosynchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="4483b-495">Per impostazione predefinita, AzCopy esegue la copia in modo asincrono sul lato server.</span><span class="sxs-lookup"><span data-stu-id="4483b-495">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="4483b-496">Specificare questa opzione tooperform sincrona copia, che scarica BLOB o i file di memoria toolocal e quindi li carica tooAzure archiviazione.</span><span class="sxs-lookup"><span data-stu-id="4483b-496">Specify this option tooperform a synchronous copy, which downloads blobs or files toolocal memory and then uploads them tooAzure Storage.</span></span>

<span data-ttu-id="4483b-497">È possibile utilizzare questa opzione quando si copiano file nell'archiviazione Blob, all'interno di archiviazione di File o da Blob archiviazione tooFile archiviazione o vice versa.</span><span class="sxs-lookup"><span data-stu-id="4483b-497">You can use this option when copying files within Blob storage, within File storage, or from Blob storage tooFile storage or vice versa.</span></span>

<span data-ttu-id="4483b-498">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="4483b-498">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="4483b-499">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="4483b-499">/SetContentType:"content-type"</span></span>
<span data-ttu-id="4483b-500">Specifica tipo di contenuto MIME hello per BLOB di destinazione o i file.</span><span class="sxs-lookup"><span data-stu-id="4483b-500">Specifies hello MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="4483b-501">Set di AzCopy hello tipo di contenuto per un blob o il file tooapplication/octet-stream per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4483b-501">AzCopy sets hello content type for a blob or file tooapplication/octet-stream by default.</span></span> <span data-ttu-id="4483b-502">Specificando in modo esplicito un valore per questa opzione, è possibile impostare tipo di contenuto per tutti i BLOB o i file hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-502">You can set hello content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="4483b-503">Se si specifica questa opzione senza un valore, AzCopy imposterà ogni blob o il tipo di contenuto del file in base a tooits estensione di file.</span><span class="sxs-lookup"><span data-stu-id="4483b-503">If you specify this option without a value, then AzCopy will set each blob or file's content type according tooits file extension.</span></span>

<span data-ttu-id="4483b-504">**Applicabile a:** BLOB, file</span><span class="sxs-lookup"><span data-stu-id="4483b-504">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="4483b-505">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="4483b-505">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="4483b-506">Specifica il formato di hello hello tabella esportata del file di dati.</span><span class="sxs-lookup"><span data-stu-id="4483b-506">Specifies hello format of hello table exported data file.</span></span>

<span data-ttu-id="4483b-507">Se questa opzione non è specificata, per impostazione predefinita AzCopy esporta il file di dati tabella nel formato JSON.</span><span class="sxs-lookup"><span data-stu-id="4483b-507">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="4483b-508">**Applicabile a:** tabelle</span><span class="sxs-lookup"><span data-stu-id="4483b-508">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="4483b-509">Problemi noti e procedure consigliate</span><span class="sxs-lookup"><span data-stu-id="4483b-509">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="4483b-510">Limitare le scritture simultanee durante la copia dei dati</span><span class="sxs-lookup"><span data-stu-id="4483b-510">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="4483b-511">Quando si copiano BLOB o i file con AzCopy, tenere presente che un'altra applicazione può modificare dati hello mentre si copiano.</span><span class="sxs-lookup"><span data-stu-id="4483b-511">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying hello data while you are copying it.</span></span> <span data-ttu-id="4483b-512">Se possibile, verificare che i dati di hello che si copia non viene modificati durante l'operazione di copia hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-512">If possible, ensure that hello data you are copying is not being modified during hello copy operation.</span></span> <span data-ttu-id="4483b-513">Ad esempio, quando si copia un disco rigido virtuale associato a una macchina virtuale di Azure, assicurarsi che altre applicazioni non sono attualmente scrivendo toohello disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="4483b-513">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing toohello VHD.</span></span> <span data-ttu-id="4483b-514">Toodo un modo efficace questa caratteristica è leasing hello risorsa toobe copiati.</span><span class="sxs-lookup"><span data-stu-id="4483b-514">A good way toodo this is by leasing hello resource toobe copied.</span></span> <span data-ttu-id="4483b-515">In alternativa, è possibile creare uno snapshot del disco rigido virtuale hello prima e quindi copiare hello snapshot.</span><span class="sxs-lookup"><span data-stu-id="4483b-515">Alternately, you can create a snapshot of hello VHD first and then copy hello snapshot.</span></span>

<span data-ttu-id="4483b-516">Se non è possibile impedire o la scrittura tooblobs file mentre vengono copiate, quindi tenere presente che, dal processo di hello hello tempo al termine di altre applicazioni, hello copiate risorse possono non avere completa parità con le risorse dell'origine hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-516">If you cannot prevent other applications from writing tooblobs or files while they are being copied, then keep in mind that by hello time hello job finishes, hello copied resources may no longer have full parity with hello source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="4483b-517">Eseguire un'istanza di AzCopy su un computer.</span><span class="sxs-lookup"><span data-stu-id="4483b-517">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="4483b-518">AzCopy è progettato toomaximize hello utilizzo del computer risorse tooaccelerate hello di trasferimento dei dati, è consigliabile eseguire solo un'istanza di AzCopy in un computer e specificare l'opzione hello `/NC` se è necessario simultanea di più operazioni.</span><span class="sxs-lookup"><span data-stu-id="4483b-518">AzCopy is designed toomaximize hello utilization of your machine resource tooaccelerate hello data transfer, we recommend you run only one AzCopy instance on one machine, and specify hello option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="4483b-519">Per ulteriori informazioni, digitare `AzCopy /?:NC` nella riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="4483b-519">For more details, type `AzCopy /?:NC` at hello command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="4483b-520">Abilitare gli algoritmi MD5 conformi a FIPS per AzCopy quando si utilizzano gli algoritmi FIPS compatibili per crittografia, hash e firma.</span><span class="sxs-lookup"><span data-stu-id="4483b-520">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="4483b-521">AzCopy per impostazione predefinita utilizza hello toocalculate di implementazione .NET MD5 MD5 durante la copia di oggetti, ma esistono alcuni requisiti di sicurezza che richiedono l'impostazione MD5 compatibile di AzCopy tooenable FIPS.</span><span class="sxs-lookup"><span data-stu-id="4483b-521">AzCopy by default uses .NET MD5 implementation toocalculate hello MD5 when copying objects, but there are some security requirements that need AzCopy tooenable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="4483b-522">È possibile creare un file app.config `AzCopy.exe.config` con la proprietà `AzureStorageUseV1MD5` e conservarlo con AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="4483b-522">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="4483b-523">Per la proprietà "AzureStorageUseV1MD5" • True: valore predefinito di hello, AzCopy utilizzerà implementazione .NET MD5.</span><span class="sxs-lookup"><span data-stu-id="4483b-523">For property "AzureStorageUseV1MD5" • True - hello default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="4483b-524">• False: AzCopy utilizzerà l'algoritmo MD5 conforme a FIPS.</span><span class="sxs-lookup"><span data-stu-id="4483b-524">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="4483b-525">Si noti che gli algoritmi conformi a FIPS sono disabilitati per impostazione predefinita nel computer Windows. Digitare secpol.msc nella finestra Esegui e selezionare questa opzione in Impostazione di sicurezza -> Criteri locali -> Opzioni di sicurezza -> Crittografia di sistema: utilizza algoritmi FIPS compatibili per crittografia, hash e firma.</span><span class="sxs-lookup"><span data-stu-id="4483b-525">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4483b-526">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4483b-526">Next steps</span></span>
<span data-ttu-id="4483b-527">Per ulteriori informazioni sull'archiviazione di Azure e AzCopy, vedere toohello seguenti risorse.</span><span class="sxs-lookup"><span data-stu-id="4483b-527">For more information about Azure Storage and AzCopy, refer toohello following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="4483b-528">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4483b-528">Azure Storage documentation:</span></span>
* [<span data-ttu-id="4483b-529">Introduzione tooAzure archiviazione</span><span class="sxs-lookup"><span data-stu-id="4483b-529">Introduction tooAzure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="4483b-530">Come toouse archiviazione Blob da .NET</span><span class="sxs-lookup"><span data-stu-id="4483b-530">How toouse Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="4483b-531">Come toouse archiviazione di File da .NET</span><span class="sxs-lookup"><span data-stu-id="4483b-531">How toouse File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="4483b-532">Come toouse archiviazione tabelle da .NET</span><span class="sxs-lookup"><span data-stu-id="4483b-532">How toouse Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="4483b-533">Come toocreate, gestire o eliminare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="4483b-533">How toocreate, manage, or delete a storage account</span></span>](storage-create-storage-account.md)
* [<span data-ttu-id="4483b-534">Trasferire dati con AzCopy in Linux</span><span class="sxs-lookup"><span data-stu-id="4483b-534">Transfer data with AzCopy on Linux</span></span>](storage-use-azcopy-linux.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="4483b-535">Post del blog di Archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="4483b-535">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="4483b-536">Introduzione alla versione di anteprima della libreria per lo spostamento dei dati di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="4483b-536">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="4483b-537">AzCopy: introduzione alla copia sincrona e al tipo di contenuto personalizzato</span><span class="sxs-lookup"><span data-stu-id="4483b-537">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="4483b-538">AzCopy: annuncio della disponibilità per tutti di AzCopy 3.0 oltre alla versione di anteprima di AzCopy 4.0 con il supporto di tabelle e file</span><span class="sxs-lookup"><span data-stu-id="4483b-538">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="4483b-539">AzCopy: ottimizzazione per gli scenari di copia su larga scala</span><span class="sxs-lookup"><span data-stu-id="4483b-539">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="4483b-540">AzCopy:supporto per l'archiviazione con ridondanza geografica e accesso in lettura</span><span class="sxs-lookup"><span data-stu-id="4483b-540">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="4483b-541">AzCopy:trasferimento di dati con modalità riavviabile e token di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="4483b-541">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="4483b-542">AzCopy: uso del comando di copia dei BLOB tra account</span><span class="sxs-lookup"><span data-stu-id="4483b-542">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="4483b-543">AzCopy: Caricamento e download di file per BLOB di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4483b-543">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

