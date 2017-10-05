---
title: Come usare PowerShell per gestire Archiviazione file di Azure| Microsoft Docs
description: Informazioni su come usare PowerShell per gestire Archiviazione file di Azure.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: ce62d4423ce711a6902aed7b8174ff4e827f6083
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-powershell-to-manage-azure-file-storage"></a><span data-ttu-id="64772-103">Come usare PowerShell per gestire Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="64772-103">How to use PowerShell to manage Azure File storage</span></span>
<span data-ttu-id="64772-104">È possibile usare Azure PowerShell per creare e gestire le condivisioni file.</span><span class="sxs-lookup"><span data-stu-id="64772-104">You can use Azure PowerShell to create and manage file shares.</span></span>

## <a name="install-the-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="64772-105">Installare i cmdlet di PowerShell per l'archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="64772-105">Install the PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="64772-106">Per prepararsi all'uso di PowerShell, scaricare e installare i cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64772-106">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="64772-107">Vedere [Come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) per le istruzioni relative al punto di installazione e all’installazione.</span><span class="sxs-lookup"><span data-stu-id="64772-107">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="64772-108">Si consiglia di scaricare e installare oppure aggiornare il modulo alla versione di Azure PowerShell più recente.</span><span class="sxs-lookup"><span data-stu-id="64772-108">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="64772-109">Per aprire una finestra di Azure PowerShell, fare clic su **Start** e digitare **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="64772-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="64772-110">La finestra di PowerShell carica automaticamente il modulo Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64772-110">The PowerShell window loads the Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="64772-111">Creare un contesto per l'account e la chiave di archiviazione</span><span class="sxs-lookup"><span data-stu-id="64772-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="64772-112">Creare il contesto dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="64772-112">Create the storage account context.</span></span> <span data-ttu-id="64772-113">Il contesto incapsula il nome e la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="64772-113">The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="64772-114">Per istruzioni sulla copia della chiave dell'account dal [portale di Azure](https://portal.azure.com), vedere [Visualizzare e copiare le chiavi di accesso alle risorse di archiviazione](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="64772-114">For instructions on copying your account key from the [Azure portal](https://portal.azure.com), see [View and copy storage access keys](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="64772-115">Sostituire `storage-account-name` e `storage-account-key` con il nome e la chiave dell'account di archiviazione nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="64772-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in the following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="64772-116">Creare una nuova condivisione file</span><span class="sxs-lookup"><span data-stu-id="64772-116">Create a new file share</span></span>
<span data-ttu-id="64772-117">Creare la nuova condivisione, denominata `logs`.</span><span class="sxs-lookup"><span data-stu-id="64772-117">Create the new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="64772-118">A questo punto si ha una condivisione file nell'archiviazione file.</span><span class="sxs-lookup"><span data-stu-id="64772-118">You now have a file share in File storage.</span></span> <span data-ttu-id="64772-119">Vengono quindi aggiunti un file e una directory.</span><span class="sxs-lookup"><span data-stu-id="64772-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64772-120">Il nome della condivisione file deve essere composto solo da caratteri minuscoli.</span><span class="sxs-lookup"><span data-stu-id="64772-120">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="64772-121">Per dettagli su come denominare condivisioni e file, vedere [Denominazione e riferimento a condivisioni, directory, file e metadati](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="64772-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-the-file-share"></a><span data-ttu-id="64772-122">Creare una directory nella condivisione file</span><span class="sxs-lookup"><span data-stu-id="64772-122">Create a directory in the file share</span></span>
<span data-ttu-id="64772-123">Creare una directory nella condivisione.</span><span class="sxs-lookup"><span data-stu-id="64772-123">Create a directory in the share.</span></span> <span data-ttu-id="64772-124">Nell'esempio seguente la directory è denominata `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="64772-124">In the following example, the directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in the share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-to-the-directory"></a><span data-ttu-id="64772-125">Caricare un file locale nella directory</span><span class="sxs-lookup"><span data-stu-id="64772-125">Upload a local file to the directory</span></span>
<span data-ttu-id="64772-126">Caricare un file locale nella directory.</span><span class="sxs-lookup"><span data-stu-id="64772-126">Now upload a local file to the directory.</span></span> <span data-ttu-id="64772-127">Nel seguente esempio viene caricato un file da `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="64772-127">The following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="64772-128">Modificare il percorso del file in modo che punti a un file valido nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="64772-128">Edit the file path so that it points to a valid file on your local machine.</span></span>

```powershell
# upload a local file to the new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-the-files-in-the-directory"></a><span data-ttu-id="64772-129">Elencare i file nella directory</span><span class="sxs-lookup"><span data-stu-id="64772-129">List the files in the directory</span></span>
<span data-ttu-id="64772-130">Per visualizzare un file nella directory, è possibile elencare tutti i file della directory.</span><span class="sxs-lookup"><span data-stu-id="64772-130">To see the file in the directory, you can list all of the directory's files.</span></span> <span data-ttu-id="64772-131">Questo comando restituisce file e sottodirectory, se presenti, nella directory CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="64772-131">This command returns the files and subdirectories (if there are any) in the CustomLogs directory.</span></span>

```powershell
# list files in the new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="64772-132">Get-AzureStorageFile restituisce un elenco di file e directory per qualsiasi oggetto di directory passato.</span><span class="sxs-lookup"><span data-stu-id="64772-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="64772-133">"Get-AzureStorageFile -Share $s" restituisce un elenco di file e directory nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="64772-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in the root directory.</span></span> <span data-ttu-id="64772-134">Per ottenere un elenco di file in una sottodirectory, è necessario passare la sottodirectory a Get-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="64772-134">To get a list of files in a subdirectory, you have to pass the subdirectory to Get-AzureStorageFile.</span></span> <span data-ttu-id="64772-135">La prima parte del comando fino alla pipe restituisce un'istanza di directory della sottodirectory CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="64772-135">That's what this does -- the first part of the command up to the pipe returns a directory instance of the subdirectory CustomLogs.</span></span> <span data-ttu-id="64772-136">Il comando viene quindi passato a Get-AzureStorageFile, che restituisce i file e le directory in CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="64772-136">Then that is passed into Get-AzureStorageFile, which returns the files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="64772-137">Copiare i file</span><span class="sxs-lookup"><span data-stu-id="64772-137">Copy files</span></span>
<span data-ttu-id="64772-138">A partire dalla versione 0.9.7 di Azure PowerShell, è possibile copiare un file in un altro file, un file in un BLOB o un BLOB in un file.</span><span class="sxs-lookup"><span data-stu-id="64772-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="64772-139">Di seguito viene illustrato come eseguire queste operazioni di copia con i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64772-139">Below we demonstrate how to perform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file to the new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob to a file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="64772-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="64772-140">Next steps</span></span>
<span data-ttu-id="64772-141">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="64772-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="64772-142">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="64772-142">FAQ</span></span>](../storage-files-faq.md)
* [<span data-ttu-id="64772-143">Risoluzione dei problemi in Windows</span><span class="sxs-lookup"><span data-stu-id="64772-143">Troubleshooting on Windows</span></span>](storage-troubleshoot-windows-file-connection-problems.md)      
* [<span data-ttu-id="64772-144">Risoluzione dei problemi in Linux</span><span class="sxs-lookup"><span data-stu-id="64772-144">Troubleshooting on Linux</span></span>](storage-troubleshoot-linux-file-connection-problems.md)    