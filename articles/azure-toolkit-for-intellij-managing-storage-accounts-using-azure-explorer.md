---
title: gli account di archiviazione aaaManage utilizzando hello Azure Explorer per IntelliJ | Documenti Microsoft
description: Informazioni come toomanage l'archiviazione di Azure degli account con hello Azure Explorer per IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: b094bdcd2fa2782cb12b67c96ac406fbe4c1aa3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-intellij"></a>Gestire gli account di archiviazione tramite Esplora Azure hello per IntelliJ

Hello Esplora Azure, che fa parte di Azure Toolkit per IntelliJ hello, fornisce agli sviluppatori di Java con una soluzione da usare per la gestione degli account di archiviazione nel proprio account da Azure all'interno di ambiente di sviluppo integrato (IDE) di hello IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>Creare un account di archiviazione in IntelliJ

un account di archiviazione tramite Esplora Azure hello toocreate hello seguenti:

1. Accedi tooyour account Azure tramite hello [accesso le istruzioni per hello Azure Toolkit per Eclipse]. 

2. In hello **Esplora Azure** visualizzare, espandere hello **Azure** nodo, fare doppio clic su **gli account di archiviazione**, quindi fare clic su **crea Account di archiviazione**.

   ![Comando Crea account di archiviazione][CS01]

3. In hello **crea Account di archiviazione** finestra di dialogo specificare hello le opzioni seguenti:

   ![Finestra di dialogo Crea un nuovo account di archiviazione][CS02]

   * **Nome**: Specifica il nome di hello hello nuovo account di archiviazione.

   * **Tipo di conto**: Specifica il tipo di hello di toocreate di account di archiviazione (ad esempio, "archiviazione Blob"). Per altre informazioni, vedere [Informazioni sugli account di archiviazione di Azure]. 

   * **Prestazioni**: specifica l'account di archiviazione offerta toouse dal server di pubblicazione selezionato hello (ad esempio, "Premium"). Per altre informazioni, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure]. 

   * **Replica**: specifica la replica di hello hello account di archiviazione (ad esempio, "con ridondanza della zona"). Per altre informazioni, vedere [Replica di Archiviazione di Azure]. 

   * **Sottoscrizione**: specifica sottoscrizione di Azure che si vuole toouse per il nuovo account di archiviazione hello hello.

   * **Percorso**: Specifica il percorso di hello in cui verranno creati account di archiviazione (ad esempio, "Stati Uniti occidentali").

   * **Gruppo di risorse**: Specifica il gruppo di risorse hello per la macchina virtuale. Selezionare una delle seguenti opzioni hello:
      * **Creare nuovi**: Specifica che si desidera toocreate un nuovo gruppo di risorse.
      * **Usa esistente**: specifica che sarà possibile scegliere in un elenco i gruppi di risorse associati all'account di Azure.

4. Dopo aver specificato tutti hello opzioni precedenti, fare clic su **OK**.

## <a name="create-a-storage-container-in-intellij"></a>Creare un contenitore di archiviazione in IntelliJ

un contenitore di archiviazione tramite Esplora Azure hello toocreate hello seguenti:

1. In visualizzazione di Esplora risorse di Azure hello, fare doppio clic su account di archiviazione hello in cui si desidera toocreate un contenitore e quindi fare clic su **crea contenitore blob**.

   ![Comando Crea contenitore BLOB][CC01]

2. In hello **crea contenitore blob** la finestra di dialogo, specificare nome hello per il contenitore e quindi fare clic su **OK**. Per altre informazioni sulla denominazione dei contenitori di archiviazione, vedere l'articolo relativo alla [denominazione e riferimento a contenitori, BLOB e metadati].

   ![Finestra di dialogo Crea contenitore di archiviazione][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>Eliminare un contenitore di archiviazione in IntelliJ

un contenitore di archiviazione tramite Esplora Azure hello toodelete hello seguenti:

1. In hello visualizzazione Esplora risorse di Azure, il contenitore di archiviazione hello destro e quindi fare clic su **eliminare**.

   ![Comando Elimina contenitore di archiviazione][DC01]

2. Nella finestra di conferma hello, fare clic su **Sì**.

   ![Finestra di conferma dell'eliminazione del contenitore di archiviazione][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>Eliminare un account di archiviazione in IntelliJ

un account di archiviazione tramite Esplora Azure hello toodelete hello seguenti:

1. In hello **Esplora Azure** consente di visualizzare, fare doppio clic su account di archiviazione hello e quindi selezionare **eliminare**.

   ![Menu per l'eliminazione dell'account di archiviazione][DS01]

2. Nella finestra di conferma hello, fare clic su **Sì**.

   ![Finestra di conferma dell'eliminazione dell'account di archiviazione][DS02]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sugli account di archiviazione di Azure, le dimensioni e sui prezzi, vedere hello seguenti risorse:

* [Introduzione tooMicrosoft di archiviazione di Azure]
* [Informazioni sugli account di archiviazione di Azure]
* Dimensioni degli account di archiviazione di Azure
  * [Sizes for Windows storage accounts in Azure] (Dimensioni degli account di archiviazione Windows in Azure)
  * [Sizes for Linux storage accounts in Azure] (Dimensioni degli account di archiviazione Linux in Azure)
* Prezzi per gli account di archiviazione di Azure
  * [Prezzi per gli account di archiviazione Windows]
  * [Prezzi per gli account di archiviazione Linux]

Per ulteriori informazioni su Azure Toolkit per IDE Java, vedere hello seguenti risorse:

* [Toolkit di Azure per Eclipse]
  * [Novità di hello Azure Toolkit per Eclipse]
  * [L'installazione di hello Azure Toolkit per Eclipse]
  * [Istruzioni di accesso per hello Azure Toolkit per Eclipse]
  * [Creare un'app Web Hello World per Azure in Eclipse]
* [Toolkit di Azure per IntelliJ]
  * [Novità di hello Azure Toolkit per IntelliJ]
  * [Installazione di hello Azure Toolkit per IntelliJ]
  * [Accesso le istruzioni per hello Azure Toolkit per IntelliJ]
  * [Creare un'App Web Hello World per Azure in IntelliJ]

Per altre informazioni su come usare Azure con Java, vedere il [Centro per sviluppatori Java di Azure] e gli [strumenti Java per Visual Studio Team Services].

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md
[Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creare un'app Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[L'installazione di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Istruzioni di accesso per hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Accesso le istruzioni per hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novità di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novità di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Strumenti Java per Visual Studio Team Services]: https://java.visualstudio.com/

[Introduzione tooMicrosoft di archiviazione di Azure]: /azure/storage/storage-introduction
[Informazioni sugli account di archiviazione di Azure]: /azure/storage/storage-create-storage-account
[Replica di Archiviazione di Azure]: /azure/storage/storage-redundancy
[Obiettivi di scalabilità e prestazioni per Archiviazione di Azure]: /azure/storage/storage-scalability-targets
[Denominazione e riferimento a contenitori, BLOB e metadati]: http://go.microsoft.com/fwlink/?LinkId=255555

[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes (Dimensioni degli account di archiviazione Windows in Azure)
[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes (Dimensioni degli account di archiviazione Linux in Azure)
[Prezzi per gli account di archiviazione Windows]: /pricing/details/virtual-machines/windows/
[Prezzi per gli account di archiviazione Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
