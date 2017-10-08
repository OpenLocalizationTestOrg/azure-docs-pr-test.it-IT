---
title: archiviazione di file di Azure da una macchina virtuale Windows Azure aaaMount | Documenti Microsoft
description: Archiviare i file nel cloud hello con l'archiviazione di file di Azure e montare la condivisione di file cloud da una macchina virtuale di Azure (VM).
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a>Usare le condivisioni file di Azure con le macchine virtuali Windows 

È possibile usare condivisioni di file di Azure come un modo toostore e accedere ai file dalla macchina virtuale. Ad esempio, è possibile archiviare uno script o un file di configurazione dell'applicazione che si desidera che tutti i tooshare di macchine virtuali. In questo argomento viene illustrata come condivisione di file toocreate e montaggio di Azure e come tooupload e scaricare file.

## <a name="connect-tooa-file-share-from-a-vm"></a>Connettersi tooa condivisione di file da una macchina virtuale

In questa sezione si presuppone il che hai già un file di condivisione desiderata tooconnect per. Se è necessario toocreate uno, vedere [creare una condivisione file](#create-a-file-share) più avanti in questo argomento.

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere dal menu a sinistra, hello **gli account di archiviazione**.
3. Scegliere l'account di archiviazione.
4. In hello **Panoramica** pagina **servizi**selezionare **file**.
5. Selezionare una condivisione file.
6. Fare clic su **Connetti** tooopen una pagina in cui viene illustrata la sintassi della riga di comando hello per la condivisione di file hello di montaggio da Windows o Linux.
7. Evidenziare hello sintassi del comando hello e incollarlo nel blocco note o in altre posizioni in cui è possibile accedervi facilmente. 
8. Modifica iniziali di hello hello sintassi tooremove * * > * * e sostituire *[lettera di unità]* con lettera di unità hello (ad esempio, **y:**) in cui si desidera toomount condivisione di file hello.
8. Connettersi tooyour macchina virtuale e aprire un prompt dei comandi.
9. Incolla in hello modificare la sintassi di connessione e premere **invio**.
10. Quando hello connessione è stata creata, viene visualizzato il messaggio di hello **hello comando completato.**
11. Controllare la connessione hello digitando hello lettera tooswitch toothat unità e quindi digitare **dir** contenuto hello toosee della condivisione file hello.



## <a name="create-a-file-share"></a>Creare una condivisione file 
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere dal menu a sinistra, hello **gli account di archiviazione**.
3. Scegliere l'account di archiviazione.
4. In hello **Panoramica** pagina **servizi**selezionare **file**.
5. Nella pagina del servizio File hello, fare clic su **+ condivisione File** toocreate condivisione del primo file. \
6. Inserire il nome di condivisione file hello. I nomi delle condivisioni file possono contenere lettere minuscole, numeri e trattini singoli. Hello nome non può iniziare con un trattino e non è possibile utilizzare più trattini consecutivi. 
7. Riempimento in un limite per le dimensioni file hello possibile too5120 GB.
8. Fare clic su **OK** toodeploy condivisione di file hello.
   
## <a name="upload-files"></a>Caricare file
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere dal menu a sinistra, hello **gli account di archiviazione**.
3. Scegliere l'account di archiviazione.
4. In hello **Panoramica** pagina **servizi**selezionare **file**.
5. Selezionare una condivisione file.
6. Fare clic su **caricare** tooopen hello **caricare file** pagina.
7. Fare clic su hello cartella icona toobrowse nel file system locale per tooupload un file.   
8. Fare clic su **caricare** condivisione di file toohello file hello tooupload.

## <a name="download-files"></a>Download dei file
1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Scegliere dal menu a sinistra, hello **gli account di archiviazione**.
3. Scegliere l'account di archiviazione.
4. In hello **Panoramica** pagina **servizi**selezionare **file**.
5. Selezionare una condivisione file.
6. Fare clic sul file hello e scegliere **scaricare** toodownload il computer locale tooyour.
   

## <a name="next-steps"></a>Passaggi successivi

Le condivisioni file possono essere create e gestite anche usando PowerShell. Per altre informazioni, vedere [Introduzione ad Archiviazione file di Azure in Windows](../../storage/files/storage-dotnet-how-to-use-files.md).
