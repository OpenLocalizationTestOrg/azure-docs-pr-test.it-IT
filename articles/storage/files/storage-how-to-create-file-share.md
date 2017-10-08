---
title: aaaHow toocreate una condivisione di File di Azure | Documenti Microsoft
description: Toocreate come un file di Azure condividere in archiviazione di File di Azure utilizzando hello portale di Azure, PowerShell e hello CLI di Azure.
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
ms.openlocfilehash: 816694e411a993dae881816fc62173e2b7afe990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>Creare una condivisione file in Archiviazione file di Azure
È possibile creare condivisioni di File di Azure utilizzando [portale di Azure](https://portal.azure.com/), hello cmdlet PowerShell di archiviazione di Azure, hello librerie client di archiviazione di Azure o hello API REST di archiviazione di Azure. In questa esercitazione si apprenderà:
* [Come toocreate un File di Azure condividono utilizzando hello portale di Azure](#Create file share through hello Portal)
* [Come toocreate un File di Azure condividono con Powershell](#Create file share using PowerShell)
* [Come toocreate un File di Azure condividono utilizzando CLI](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>Prerequisiti
toocreate una condivisione di File di Azure, è possibile utilizzare un account di archiviazione già esistente, o [creare un nuovo account di archiviazione di Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json). toocreate una condivisione di File di Azure con PowerShell, è necessario hello account chiave e il nome dell'account di archiviazione... Chiave dell'account di archiviazione è necessario se si prevede di toouse Powershell o CLI.

## <a name="create-file-share-through-hello-portal"></a>Creare la condivisione di file tramite hello portale
1. **Pannello Account tooStorage andare nel portale di Azure**:    
    ![Pannello Account di archiviazione](./media/storage-how-to-create-file-share/create-file-share-portal1.png)

2. **Fare clic sul pulsante Aggiungi condivisione file**:    
    ![Fare clic su hello aggiungere il pulsante di condivisione file](./media/storage-how-to-create-file-share/create-file-share-portal2.png)

3. **Specificare il nome e la quota. La quota attualmente non può essere superiore a 5 TB**:    
    ![Specificare un nome e una quota desiderata per la nuova condivisione di file hello](./media/storage-how-to-create-file-share/create-file-share-portal3.png)

4. **Visualizzare la nuova condivisione file**: ![Visualizzare la nuova condivisione file](./media/storage-how-to-create-file-share/create-file-share-portal4.png)

5. **Caricare un file**: ![Caricare un file](./media/storage-how-to-create-file-share/create-file-share-portal5.png)

6. **Esplorare la condivisione file e gestire le directory e i file**: ![Esplorare la condivisione file](./media/storage-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>Creare la condivisione file tramite PowerShell
tooprepare toouse PowerShell, scaricare e installare i cmdlet di Azure PowerShell hello. Vedere [come tooinstall e configurare Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) per hello installare istruzioni sull'installazione e punto.

> [!Note]  
> È consigliabile scaricare e installare o aggiornare il modulo PowerShell di Azure più recente di toohello.

1. **Creare un contesto per l'account di archiviazione e la chiave** contesto hello incapsula hello chiave account di archiviazione nome e all'account. Per istruzioni sulla copia della chiave dell'account dal [portale di Azure](https://portal.azure.com/), vedere [Visualizzare e copiare le chiavi di accesso alle risorse di archiviazione](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **Creare una nuova condivisione file**:    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> nome Hello della condivisione file deve essere tutti in lettere minuscole. Per dettagli su come denominare condivisioni e file, vedere [Denominazione e riferimento a condivisioni, directory, file e metadati](https://msdn.microsoft.com/library/azure/dn167011.aspx).

## <a name="create-file-share-through-command-line-interface-cli"></a>Creare una condivisione file tramite l'interfaccia della riga di comando
1. **tooprepare toouse interfaccia della riga di comando (CLI), scaricare e installare hello CLI di Azure.**  
    Vedere [Installare l'interfaccia della riga di comando di Azure 2.0](/cli/azure/install-az-cli2.md) e [Introduzione all'interfaccia della riga di comando di Azure 2.0](/cli/azure/get-started-with-azure-cli.md).

2. **Creare un account di archiviazione toohello di stringa di connessione in cui si desidera condivisione hello toocreate.**  
    Sostituire ```<storage-account>``` e ```<resource_group>``` con l'account nome e la risorsa gruppo di archiviazione nel seguente esempio hello.

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. **Creare la condivisione file**
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>Passaggi successivi
* [Connettersi e montare una condivisione file: Windows](storage-how-to-use-files-windows.md)
* [Connettersi e montare una condivisione file: Linux](../storage-how-to-use-files-linux.md)
* [Connettersi e montare una condivisione file: macOS](storage-how-to-use-files-mac.md)

Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.

* [Domande frequenti](../storage-files-faq.md)
* [Risoluzione dei problemi in Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Risoluzione dei problemi in Linux](storage-troubleshoot-linux-file-connection-problems.md)   