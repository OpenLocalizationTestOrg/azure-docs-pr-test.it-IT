---
title: aaaMove tooand di dati dall'archiviazione Blob di Azure tramite AzCopy | Documenti Microsoft
description: Spostare dati tooand dall'archiviazione Blob di Azure tramite AzCopy
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a>Spostare dati tooand dall'archiviazione Blob di Azure tramite AzCopy
AzCopy è un'utilità della riga di comando progettata per il caricamento, download e copia tooand dati dal blob, file e archiviazione tabelle di Microsoft Azure.

Per istruzioni sull'installazione di AzCopy e informazioni aggiuntive sull'utilizzo con hello piattaforma Azure, vedere [introduzione hello utilità della riga di comando di AzCopy](../storage/common/storage-use-azcopy.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Se si utilizza macchina virtuale che è stato configurato con gli script hello disponibili in [macchine virtuali di analisi scientifica dei dati in Azure](machine-learning-data-science-virtual-machines.md), quindi AzCopy è già installata nella macchina virtuale hello.
> 
> [!NOTE]
> Per un'archiviazione blob tooAzure introduzione completa, vedere troppo[nozioni fondamentali di Blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e troppo[servizio Blob di Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Questo documento presuppone di disporre di una sottoscrizione di Azure, un account di archiviazione e hello chiave di archiviazione corrispondente per tale account. Prima di caricare/scaricare i dati, è necessario conoscere il nome e la chiave del proprio account di archiviazione di Azure.

* tooset di una sottoscrizione di Azure, vedere [la versione di un mese valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Per istruzioni sulla creazione di un account di archiviazione e per ottenere informazioni sull’account e la chiave, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).

## <a name="run-azcopy-commands"></a>Eseguire i comandi di AzCopy
comandi AzCopy toorun, aprire una finestra di comando e passare toohello AzCopy directory di installazione nel computer in cui si trova l'eseguibile AzCopy.exe hello. 

sintassi di base per i comandi AzCopy Hello è:

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> È possibile aggiungere hello AzCopy tooyour sistema percorso di installazione e quindi eseguire i comandi di hello da qualsiasi directory. Per impostazione predefinita, AzCopy è installato troppo*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* o *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.
> 
> 

## <a name="upload-files-tooan-azure-blob"></a>Caricare file tooan blob di Azure
tooupload un file, utilizzare hello comando seguente:

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a>Scaricare file da un BLOB di Azure
toodownload un file da un blob di Azure, utilizzare hello comando seguente:

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a>Trasferire i BLOB tra contenitori di Azure
BLOB tootransfer tra i contenitori di Azure, utilizzare hello comando seguente:

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a>Suggerimenti per l'utilizzo di AzCopy
> [!TIP]
> 1. Quando si **caricano** file, */S* caricherà i file in modo ricorsivo. Senza questo parametro, i file nelle sottodirectory non vengono caricati.  
> 2. Quando **download** file */S* ricerche hello contenitore in modo ricorsivo fino a quando tutti i file nella directory specificata hello e nelle relative sottodirectory, o tutti i file corrispondenti hello modello specificato in hello specificato Directory e nelle relative sottodirectory, vengono scaricati.  
> 3. Non è possibile specificare un **file blob specifico** toodownload utilizzando hello */origine* parametro. toodownload un file specifico, specificare toodownload nome file blob di hello utilizzando hello *modello/* parametro. **/S** parametro può essere utilizzato toohave AzCopy cercare un nome di file modello in modo ricorsivo. Senza il parametro di modello hello, AzCopy di scaricare tutti i file in tale directory.
> 
> 

