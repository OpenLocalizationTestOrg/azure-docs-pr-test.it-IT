---
title: aaaMove tooand di dati dall'archiviazione Blob con Esplora archivi Azure | Documenti Microsoft
description: Spostare dati tooand dall'archiviazione Blob di Azure tramite Esplora archivi Azure
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 10bd283f-0875-4c67-af63-6492270b7656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 38d3bc009950c97d8474b0acceaf74814638dac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azure-storage-explorer"></a>Spostare dati tooand dall'archiviazione Blob di Azure tramite Esplora archivi Azure
Azure Storage Explorer è uno strumento gratuito di Microsoft che consentono di toowork con i dati di archiviazione di Azure in Windows, macOS e Linux. Questo argomento viene descritto come toouse, tooupload e scaricare dati da Azure nell'archiviazione blob. strumento Hello può essere scaricato da [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Se si utilizza macchina virtuale che è stato configurato con gli script hello disponibili in [macchine virtuali di analisi scientifica dei dati in Azure](machine-learning-data-science-virtual-machines.md), quindi Esplora archivi Azure è già installato in hello macchina virtuale.
> 
> [!NOTE]
> Per un'archiviazione blob tooAzure introduzione completa, vedere troppo[nozioni fondamentali di Blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e [servizio Blob di Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).   
> 
> 

## <a name="prerequisites"></a>Prerequisiti
Questo documento si presuppone la presenza di una sottoscrizione di Azure, un account di archiviazione e chiave di archiviazione per l'account corrispondente hello. Prima di caricare/scaricare i dati, è necessario conoscere il nome e la chiave del proprio account di archiviazione di Azure. 

* tooset di una sottoscrizione di Azure, vedere [la versione di un mese valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Per istruzioni sulla creazione di un account di archiviazione e per ottenere informazioni sull’account e la chiave, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md). Rendere una chiave di accesso hello nota dell'account di archiviazione è necessario questo account toohello tooconnect chiave con lo strumento di hello Azure Storage Explorer.
* strumento di Hello Azure Storage Explorer può essere scaricato da [Microsoft Azure Storage Explorer](http://storageexplorer.com/). Accettare i valori predefiniti di hello durante l'installazione.

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a>Utilizzo di Esplora archivi Azure
Hello seguente come documento passaggi tooupload e scaricare dati tramite Esplora archivi Azure. 

1. Avviare Esplora archivi di Microsoft Azure.
2. toobring backup hello **Accedi account tooyour...**  procedura guidata, selezionare **le impostazioni dell'account Azure** icona, quindi **aggiungere un account** e immettere le credenziali. ![Aggiungere un account di archiviazione di Azure](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)
3. toobring backup hello **connettersi tooAzure archiviazione** procedura guidata, seleziona hello **connettere archiviazione tooAzure** icona. ![La connessione di archiviazione tooAzure](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)
4. Immettere la chiave di accesso hello dall'account di archiviazione di Azure in hello **connettersi tooAzure archiviazione** procedura guidata e quindi **Avanti**. ![La connessione di archiviazione tooAzure](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)
5. Immettere il nome di account di archiviazione in hello **nome Account** casella e quindi selezionare **Avanti**. ![Associa archiviazione esterna](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)
6. aggiungere l'account di archiviazione Hello dovrebbe ora essere elencato. toocreate un contenitore blob in un account di archiviazione, fare doppio clic su hello **contenitori Blob** nodo in tale account, selezionare **crea contenitore Blob**, immettere un nome.
7. contenitore di tooa dati tooupload, hello contenitore e fare clic su di destinazione selezionare hello **caricare** pulsante.![ Account di archiviazione](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)
8. Fare clic su hello **...**  toohello diritto di hello **file** , selezionare uno o più tooupload file dal file system di hello e fare clic su **caricare** toobegin caricamento file hello.![ Caricare file](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)
9. dati toodownload, selezionando hello blob in toodownload contenitore corrispondente hello e fare clic su **scaricare**. ![Download dei file](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)

