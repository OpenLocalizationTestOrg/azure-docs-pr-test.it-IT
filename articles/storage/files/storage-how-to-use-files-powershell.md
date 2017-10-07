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
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a>Come toouse PowerShell toomanage archiviazione di File di Azure
È possibile usare Azure PowerShell toocreate e gestire le condivisioni di file.

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a>Installare i cmdlet di PowerShell hello per l'archiviazione di Azure
tooprepare toouse PowerShell, scaricare e installare i cmdlet di Azure PowerShell hello. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) per hello installare istruzioni sull'installazione e punto.

> [!NOTE]
> È consigliabile scaricare e installare o aggiornare il modulo PowerShell di Azure più recente di toohello.
> 
> 

Per aprire una finestra di Azure PowerShell, fare clic su **Start** e digitare **Windows PowerShell**. finestra di PowerShell Hello carica il modulo di Azure Powershell hello automaticamente.

## <a name="create-a-context-for-your-storage-account-and-key"></a>Creare un contesto per l'account e la chiave di archiviazione
Creare il contesto di account di archiviazione hello. contesto Hello incapsula hello chiave account di archiviazione nome e all'account. Per istruzioni su come copiare la chiave dell'account da hello [portale di Azure](https://portal.azure.com), vedere [chiavi di accesso di archiviazione di visualizzazione e copia](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).

Sostituire `storage-account-name` e `storage-account-key` con il nome account di archiviazione e la chiave nel seguente esempio hello.

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a>Creare una nuova condivisione file
Crea nuova condivisione hello, denominato `logs`.

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

A questo punto si ha una condivisione file nell'archiviazione file. Vengono quindi aggiunti un file e una directory.

> [!IMPORTANT]
> nome Hello della condivisione file deve essere tutti in lettere minuscole. Per dettagli su come denominare condivisioni e file, vedere [Denominazione e riferimento a condivisioni, directory, file e metadati](https://msdn.microsoft.com/library/azure/dn167011.aspx).
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a>Creare una directory nella condivisione di file hello
Creare una directory nella condivisione di hello. Nell'esempio seguente di hello, denominato directory hello `CustomLogs`.

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a>Caricare un file locale toohello una directory
Caricare un file locale toohello una directory. esempio Hello carica un file da `C:\temp\Log1.txt`. Modificare il percorso del file hello in modo che punti tooa file valido sul computer locale.

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a>Elencare i file nella directory hello hello
file di hello toosee nella directory di hello, è possibile elencare tutti i file della directory hello. Questo comando restituisce le sottodirectory e file hello se (esistono eventuali) nella directory CustomLogs hello.

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

Get-AzureStorageFile restituisce un elenco di file e directory per qualsiasi oggetto di directory passato. "Get-AzureStorageFile-condividere $s" restituisce un elenco di file e directory nella directory radice hello. tooget un elenco di file in una sottodirectory, è necessario toopass hello sottodirectory tooGet-AzureStorageFile. In questo modo è: hello prima parte del comando hello della pipe toohello restituisce un'istanza di directory della sottodirectory hello CustomLogs. Che viene quindi passato Get-AzureStorageFile, che restituisce CustomLogs hello file e directory.

## <a name="copy-files"></a>Copiare i file
A partire dalla versione 0.9.7 di Azure PowerShell, è possibile copiare un file con estensione tooanother, un blob tooa file o un file di blob tooa. Di seguito viene illustrato come questi tooperform copiare operazioni utilizzando i cmdlet di PowerShell.

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a>Passaggi successivi
Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.

* [Domande frequenti](../storage-files-faq.md)
* [Risoluzione dei problemi in Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Risoluzione dei problemi in Linux](storage-troubleshoot-linux-file-connection-problems.md)    