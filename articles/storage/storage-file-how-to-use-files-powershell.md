---
title: aaaHow toouse PowerShell toomanage archiviazione di File di Azure | Documenti Microsoft
description: Informazioni su archiviazione di File di Azure toouse PowerShell toomanage.
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
ms.openlocfilehash: 0e30e8796cf8bbf5f9249b26179d5e0f9077c8fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a><span data-ttu-id="ea688-103">Come toouse PowerShell toomanage archiviazione di File di Azure</span><span class="sxs-lookup"><span data-stu-id="ea688-103">How toouse PowerShell toomanage Azure File storage</span></span>
<span data-ttu-id="ea688-104">È possibile usare Azure PowerShell toocreate e gestire le condivisioni di file.</span><span class="sxs-lookup"><span data-stu-id="ea688-104">You can use Azure PowerShell toocreate and manage file shares.</span></span>

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="ea688-105">Installare i cmdlet di PowerShell hello per l'archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ea688-105">Install hello PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="ea688-106">tooprepare toouse PowerShell, scaricare e installare i cmdlet di Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ea688-106">tooprepare toouse PowerShell, download and install hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="ea688-107">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) per hello installare istruzioni sull'installazione e punto.</span><span class="sxs-lookup"><span data-stu-id="ea688-107">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for hello install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="ea688-108">È consigliabile scaricare e installare o aggiornare il modulo PowerShell di Azure più recente di toohello.</span><span class="sxs-lookup"><span data-stu-id="ea688-108">It's recommended that you download and install or upgrade toohello latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="ea688-109">Per aprire una finestra di Azure PowerShell, fare clic su **Start** e digitare **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ea688-109">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="ea688-110">finestra di PowerShell Hello carica il modulo di Azure Powershell hello automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ea688-110">hello PowerShell window loads hello Azure Powershell module for you.</span></span>

## <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="ea688-111">Creare un contesto per l'account e la chiave di archiviazione</span><span class="sxs-lookup"><span data-stu-id="ea688-111">Create a context for your storage account and key</span></span>
<span data-ttu-id="ea688-112">Creare il contesto di account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="ea688-112">Create hello storage account context.</span></span> <span data-ttu-id="ea688-113">contesto Hello incapsula hello chiave account di archiviazione nome e all'account.</span><span class="sxs-lookup"><span data-stu-id="ea688-113">hello context encapsulates hello storage account name and account key.</span></span> <span data-ttu-id="ea688-114">Per istruzioni su come copiare la chiave dell'account da hello [portale di Azure](https://portal.azure.com), vedere [chiavi di accesso di archiviazione di visualizzazione e copia](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="ea688-114">For instructions on copying your account key from hello [Azure portal](https://portal.azure.com), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="ea688-115">Sostituire `storage-account-name` e `storage-account-key` con il nome account di archiviazione e la chiave nel seguente esempio hello.</span><span class="sxs-lookup"><span data-stu-id="ea688-115">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in hello following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a><span data-ttu-id="ea688-116">Creare una nuova condivisione file</span><span class="sxs-lookup"><span data-stu-id="ea688-116">Create a new file share</span></span>
<span data-ttu-id="ea688-117">Crea nuova condivisione hello, denominato `logs`.</span><span class="sxs-lookup"><span data-stu-id="ea688-117">Create hello new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="ea688-118">A questo punto si ha una condivisione file nell'archiviazione file.</span><span class="sxs-lookup"><span data-stu-id="ea688-118">You now have a file share in File storage.</span></span> <span data-ttu-id="ea688-119">Vengono quindi aggiunti un file e una directory.</span><span class="sxs-lookup"><span data-stu-id="ea688-119">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea688-120">nome Hello della condivisione file deve essere tutti in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="ea688-120">hello name of your file share must be all lowercase.</span></span> <span data-ttu-id="ea688-121">Per dettagli su come denominare condivisioni e file, vedere [Denominazione e riferimento a condivisioni, directory, file e metadati](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea688-121">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a><span data-ttu-id="ea688-122">Creare una directory nella condivisione di file hello</span><span class="sxs-lookup"><span data-stu-id="ea688-122">Create a directory in hello file share</span></span>
<span data-ttu-id="ea688-123">Creare una directory nella condivisione di hello.</span><span class="sxs-lookup"><span data-stu-id="ea688-123">Create a directory in hello share.</span></span> <span data-ttu-id="ea688-124">Nell'esempio seguente di hello, denominato directory hello `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="ea688-124">In hello following example, hello directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a><span data-ttu-id="ea688-125">Caricare un file locale toohello una directory</span><span class="sxs-lookup"><span data-stu-id="ea688-125">Upload a local file toohello directory</span></span>
<span data-ttu-id="ea688-126">Caricare un file locale toohello una directory.</span><span class="sxs-lookup"><span data-stu-id="ea688-126">Now upload a local file toohello directory.</span></span> <span data-ttu-id="ea688-127">esempio Hello carica un file da `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="ea688-127">hello following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="ea688-128">Modificare il percorso del file hello in modo che punti tooa file valido sul computer locale.</span><span class="sxs-lookup"><span data-stu-id="ea688-128">Edit hello file path so that it points tooa valid file on your local machine.</span></span>

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a><span data-ttu-id="ea688-129">Elencare i file nella directory hello hello</span><span class="sxs-lookup"><span data-stu-id="ea688-129">List hello files in hello directory</span></span>
<span data-ttu-id="ea688-130">file di hello toosee nella directory di hello, è possibile elencare tutti i file della directory hello.</span><span class="sxs-lookup"><span data-stu-id="ea688-130">toosee hello file in hello directory, you can list all of hello directory's files.</span></span> <span data-ttu-id="ea688-131">Questo comando restituisce le sottodirectory e file hello se (esistono eventuali) nella directory CustomLogs hello.</span><span class="sxs-lookup"><span data-stu-id="ea688-131">This command returns hello files and subdirectories (if there are any) in hello CustomLogs directory.</span></span>

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="ea688-132">Get-AzureStorageFile restituisce un elenco di file e directory per qualsiasi oggetto di directory passato.</span><span class="sxs-lookup"><span data-stu-id="ea688-132">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="ea688-133">"Get-AzureStorageFile-condividere $s" restituisce un elenco di file e directory nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="ea688-133">"Get-AzureStorageFile -Share $s" returns a list of files and directories in hello root directory.</span></span> <span data-ttu-id="ea688-134">tooget un elenco di file in una sottodirectory, è necessario toopass hello sottodirectory tooGet-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="ea688-134">tooget a list of files in a subdirectory, you have toopass hello subdirectory tooGet-AzureStorageFile.</span></span> <span data-ttu-id="ea688-135">In questo modo è: hello prima parte del comando hello della pipe toohello restituisce un'istanza di directory della sottodirectory hello CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="ea688-135">That's what this does -- hello first part of hello command up toohello pipe returns a directory instance of hello subdirectory CustomLogs.</span></span> <span data-ttu-id="ea688-136">Che viene quindi passato Get-AzureStorageFile, che restituisce CustomLogs hello file e directory.</span><span class="sxs-lookup"><span data-stu-id="ea688-136">Then that is passed into Get-AzureStorageFile, which returns hello files and directories in CustomLogs.</span></span>

## <a name="copy-files"></a><span data-ttu-id="ea688-137">Copiare i file</span><span class="sxs-lookup"><span data-stu-id="ea688-137">Copy files</span></span>
<span data-ttu-id="ea688-138">A partire dalla versione 0.9.7 di Azure PowerShell, è possibile copiare un file con estensione tooanother, un blob tooa file o un file di blob tooa.</span><span class="sxs-lookup"><span data-stu-id="ea688-138">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="ea688-139">Di seguito viene illustrato come questi tooperform copiare operazioni utilizzando i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ea688-139">Below we demonstrate how tooperform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a><span data-ttu-id="ea688-140">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ea688-140">Next steps</span></span>
<span data-ttu-id="ea688-141">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="ea688-141">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="ea688-142">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="ea688-142">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="ea688-143">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="ea688-143">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)