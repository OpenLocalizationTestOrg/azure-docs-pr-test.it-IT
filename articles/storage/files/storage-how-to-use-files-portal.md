---
title: aaaHow toomanage archiviazione di File di Azure dal portale di Azure hello | Documenti Microsoft
description: Informazioni su archiviazione di File di Azure toouse hello toomanage portale Azure.
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
ms.openlocfilehash: 6ad2fbbf9ee2f86748b1b175d0f63274144dc5eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a>Come archiviazione di File di Azure toouse da hello portale di Azure
Hello [portale di Azure](https://portal.azure.com) fornisce un'interfaccia utente per gestire l'archiviazione di File di Azure. È possibile eseguire hello seguente azioni dal web browser:

* Creare una condivisione file
* Caricare e scaricare file tooand dalla condivisione di file.
* Monitorare l'utilizzo effettivo di hello di ciascuna condivisione file.
* Regolare quota delle dimensioni di condivisione file hello.
* Copiare hello montaggio comandi toouse toomount condividere il file da un client di Windows o Linux.

## <a name="create-file-share"></a>Creare la condivisione file
1. Accedi toohello portale di Azure.
2. Nel menu di navigazione hello, fare clic su **gli account di archiviazione** o **gli account di archiviazione (classico)**.
    
    ![Schermata che illustra la modalità di condivisione di file toocreate nel portale di hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. Scegliere l'account di archiviazione.

    ![Schermata che illustra la modalità di condivisione di file toocreate nel portale di hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. Scegliere il servizio "File".

    ![Schermata che illustra la modalità di condivisione di file toocreate nel portale di hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. Fare clic su "Condivisioni di File" e seguire toocreate collegamento hello condivisione del primo file.

    ![Schermata che illustra la modalità di condivisione di file toocreate nel portale di hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. Immettere il nome di condivisione file hello e dimensioni hello di hello file share (backup GB too5120) toocreate condivisione file di primo. Dopo aver creata una condivisione di hello, è possibile montarlo da qualsiasi file system che supporta SMB 2.1 o SMB 3.0. È possibile fare clic su **Quota** su hello toochange hello dimensioni della condivisione file del file hello too5120 GB. Consultare troppo[calcolatore dei costi Azure](https://azure.microsoft.com/pricing/calculator/) costi di archiviazione di hello tooestimate dell'utilizzo dell'archiviazione di File di Azure.

    ![Schermata che illustra la modalità di condivisione di file toocreate nel portale di hello](./media/storage-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a>Caricare e scaricare file
1. Scegliere una condivisione file già creata.

    ![Schermata che illustra come tooupload e scaricare file da hello portale](./media/storage-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. Fare clic su **caricare** per aprire l'interfaccia utente di hello per i file di caricamento.

    ![Schermata che illustra come i file dal portale hello tooupload](./media/storage-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a>Connettersi toofile condivisione
-  Fare clic su **Connetti** per ottenere la riga di comando hello per condivisione file hello di montaggio da Windows e Linux. Per gli utenti Linux, è anche possibile fare riferimento troppo[come archiviazione di File di Azure con Linux toouse](../storage-how-to-use-files-linux.md) per ulteriori istruzioni per altre distribuzioni di Linux.

    ![Schermata che illustra come toomount hello condivisione file](./media/storage-how-to-use-files-portal/use-files-portal-connect.png)
-  È possibile copiare hello comandi per il montaggio di file di condividono in Windows o Linux ed eseguirlo da parte dell'utente macchina VM di Azure o in locale.

    ![Schermata che mostra i comandi di montaggio di hello per Windows e Linux](./media/storage-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

**Suggerimento:**  
toofind chiave di accesso account di archiviazione hello per l'installazione, fare clic su **per questo account di archiviazione delle chiavi di accesso alla visualizzazione** nella parte inferiore di hello di hello pagina Connetti.

## <a name="see-also"></a>Vedere anche
Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.

* [Domande frequenti](../storage-files-faq.md)
* [Risoluzione dei problemi in Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Risoluzione dei problemi in Linux](storage-troubleshoot-linux-file-connection-problems.md)    