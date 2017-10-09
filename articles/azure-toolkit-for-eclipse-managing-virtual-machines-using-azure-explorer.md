---
title: macchine virtuali aaaManage tramite hello Azure Explorer per Eclipse | Documenti Microsoft
description: Informazioni su come toomanage macchine virtuali di Azure tramite hello Azure Explorer per Eclipse.
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
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a>Gestire le macchine virtuali tramite hello Azure Explorer per Eclipse

Hello Esplora Azure, che fa parte di hello Azure Toolkit per Eclipse, fornisce agli sviluppatori Java una soluzione da usare per la gestione delle macchine virtuali nel proprio account da Azure all'interno di ambiente di sviluppo integrato (IDE) di hello Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a>Creare una macchina virtuale in Eclipse

una macchina virtuale utilizzando Esplora Azure hello toocreate hello seguenti:

1. Accedi tooyour account Azure tramite hello [accesso le istruzioni per hello Azure Toolkit per Eclipse].

2. In hello **Esplora Azure** visualizzare, espandere hello **Azure** nodo, fare doppio clic su **macchine virtuali**, quindi fare clic su **crea macchina virtuale**.

   ![Hello comando Crea macchina virtuale][CR01]  
   Hello **creare una nuova macchina virtuale** apre la procedura guidata.

3. In hello **scegliere una sottoscrizione** finestra, selezionare la sottoscrizione e quindi fare clic su **Avanti**.

   ![Hello finestra scegliere una sottoscrizione][CR02]

4. In hello **selezionare un'immagine di macchina virtuale** finestra immettere hello le seguenti informazioni:

   * **Località**: specifica dove verrà creata la macchina virtuale, ad esempio *Stati Uniti occidentali*.

   * **Server di pubblicazione**: specifica i server di pubblicazione di hello immagine hello userai toocreate la macchina virtuale è stata creata (ad esempio, *Microsoft*).

   * **Offrono**: specifica macchina virtuale hello offerta toouse dal server di pubblicazione selezionato hello (ad esempio, *JDK*).

   * **SKU**: hello stockkeeping prodotto (SKU) toouse dall'offerta selezionata hello specifica (ad esempio, *JDK_8*).

   * **Versione #**: specifica la versione di hello selezionato toouse SKU.

    ![Hello selezionare una finestra dell'immagine di macchina virtuale][CR03]

5. Fare clic su **Avanti**.

6. In hello **le impostazioni di base di macchina virtuale** finestra immettere hello le seguenti informazioni:

   * **Nome della macchina virtuale**: Specifica il nome di hello per la nuova macchina virtuale, che deve iniziare con una lettera e contenere solo lettere, numeri e trattini.

   * **Dimensioni**: Specifica il numero di hello di core e memoria tooallocate per la macchina virtuale.

   * **Nome utente**: hello amministratore account toocreate per la gestione della macchina virtuale specifica.

   * **Password** e **conferma**: specifica hello password per l'account amministratore.

    ![finestra Impostazioni di base di macchina virtuale Hello][CR04]

7. Fare clic su **Avanti**.

8. In hello **Crea nuovo Account di archiviazione** finestra immettere hello le seguenti informazioni:

   * **Gruppo di risorse**: Specifica il gruppo di risorse hello per la macchina virtuale. Selezionare una delle seguenti opzioni hello:
      * **Creare nuovi**: Specifica che si desidera toocreate un nuovo gruppo di risorse.
      * **Usa esistente**: Specifica che si desidera tooselect un gruppo di risorse che è già associato a un account Azure.

      ![finestra di dialogo Crea nuovo Account di archiviazione Hello][CR05]

   * **Account di archiviazione**: hello storage account toouse per archiviare la macchina virtuale specifica. È possibile usare un account di archiviazione esistente o crearne uno nuovo.

   * **Rete virtuale** e **Subnet**: specifica la rete virtuale hello e subnet che si connetterà la macchina virtuale. È possibile usare una subnet e una rete esistente oppure creare una rete e una subnet nuove. Se si seleziona **Crea nuovo**, viene visualizzata la finestra di dialogo seguente hello:

      ![finestra di dialogo Crea nuova rete virtuale Hello][CR06]

9. In hello **risorse associata** finestra immettere hello le seguenti informazioni:

   * **Indirizzo IP pubblico**: specifica un indirizzo IP con connessione esterna per la macchina virtuale. È possibile scegliere un nuovo indirizzo IP toocreate o, se la macchina virtuale non avrà un indirizzo IP pubblico, è possibile selezionare **(nessuno)**.

   * **Gruppo di sicurezza di rete**: specifica un firewall di rete facoltativo per la macchina virtuale. È possibile selezionare un firewall esistente oppure, se la macchina virtuale non usa un firewall di rete, è possibile selezionare **(Nessuno)**.

   * **Set di disponibilità**: specifica un set di disponibilità facoltativo a cui può appartenere la macchina virtuale. È possibile selezionare un set di disponibilità esistente o creare un nuovo set di disponibilità o se la macchina virtuale non apparterrà tooan set di disponibilità, è possibile selezionare **(nessuno)**.

   ![finestra di risorse associati Hello][CR07]

9. Fare clic su **Finish**.  
  La nuova macchina virtuale viene visualizzata nella finestra degli strumenti di Esplora Azure hello.

   ![Nuova macchina virtuale][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a>Riavvio di una macchina virtuale in Eclipse

una macchina virtuale utilizzando hello Esplora Azure in Eclipse, toorestart hello seguenti:

1. In hello **Esplora Azure** consente di visualizzare, fare clic sulla macchina virtuale hello e quindi selezionare **riavviare**.

   ![comando di riavvio Hello macchina virtuale][RE01]

2. Nella finestra di conferma hello, fare clic su **Sì**.

   ![finestra di conferma riavvio Hello][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a>Arrestare una macchina virtuale in Eclipse

tooshut verso il basso di una macchina virtuale in esecuzione utilizzando hello Esplora Azure in Eclipse, hello seguenti:

1. In hello **Esplora Azure** consente di visualizzare, fare clic sulla macchina virtuale hello e quindi selezionare **arresto**.

   ![comando di arresto di macchina virtuale Hello][SH01]

2. Nella finestra di conferma hello, fare clic su **Sì**.

   ![finestra di conferma di Hello arresto di macchina virtuale][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a>Eliminare una macchina virtuale in Eclipse

una macchina virtuale utilizzando hello Esplora Azure in Eclipse, toodelete hello seguenti:

1. In hello **Esplora Azure** consente di visualizzare, fare clic sulla macchina virtuale hello e quindi selezionare **eliminare**.

   ![comando di eliminazione Hello macchina virtuale][DE01]

2. Nella finestra di conferma hello, fare clic su **Sì**.

   ![finestra di conferma l'eliminazione di macchina virtuale Hello][DE02]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni sulle dimensioni di macchina virtuale di Azure e sui prezzi, vedere hello seguenti risorse:

* Dimensioni delle macchine virtuali in Azure
  * [Dimensioni per le macchine virtuali Windows in Azure]
  * [Dimensioni delle macchine virtuali Linux in Azure]
* Prezzi delle macchine virtuali in Azure
  * [Prezzi delle macchine virtuali in Windows]
  * [Prezzi delle macchine virtuali in Linux]

Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti risorse:

* [Toolkit di Azure per Eclipse]
  * [Novità di hello Azure Toolkit per Eclipse]
  * [L'installazione di hello Azure Toolkit per Eclipse]
  * [accesso le istruzioni per hello Azure Toolkit per Eclipse]
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
[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[L'installazione di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[accesso le istruzioni per hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Accesso le istruzioni per hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novità di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novità di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[strumenti Java per Visual Studio Team Services]: https://java.visualstudio.com/

[Dimensioni per le macchine virtuali Windows in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Dimensioni delle macchine virtuali Linux in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Prezzi delle macchine virtuali in Windows]: /pricing/details/virtual-machines/windows/
[Prezzi delle macchine virtuali in Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
