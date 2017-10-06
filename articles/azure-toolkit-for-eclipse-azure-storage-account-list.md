---
title: Elenco di Account di archiviazione aaaAzure
description: Gestire le impostazioni dell'account di archiviazione utilizzando hello Azure Toolkit per Eclipse
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a>Elenco di Account di archiviazione di Azure
Abilitare gli account di archiviazione Azure scaricare toobe percorsi utilizzati per il JDK, server applicazioni e componenti arbitrari, nonché per l'archiviazione dello stato quando si utilizza la memorizzazione nella cache. Eclipse gestisce un elenco di account di archiviazione conosciuti tooyour disponibili progetti nell'area di lavoro di Eclipse. hello tooopen **gli account di archiviazione** finestra di dialogo che viene utilizzato toomanage l'elenco, in Eclipse, fare clic su **finestra**, fare clic su **preferenze**, espandere **Azure** , quindi fare clic su **gli account di archiviazione**.

Hello seguente illustra la hello **gli account di archiviazione** finestra di dialogo.

![][ic719496]

Questa finestra di dialogo può anche essere aperta da un **account** collegamento nelle finestre di dialogo che utilizzano gli account di archiviazione, come illustrato di seguito hello:

* Hello **JDK** scheda di hello **configurazione Server** finestra di dialogo.
* Hello **Server** scheda di hello **configurazione Server** finestra di dialogo.
* Hello **Add Component** finestra di dialogo.
* Hello **la memorizzazione nella cache** finestra di dialogo proprietà.

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a>tooimport lo spazio di archiviazione degli account con un file di impostazioni di pubblicazione
1. All'interno di hello **gli account di archiviazione** finestra di dialogo, fare clic su **Importa da file PUBLISH-SETTINGS**.

2. (Ignorare questo passaggio se è già stato salvato un computer locale pubblica Impostazioni file tooyour). In hello **Importa informazioni sottoscrizione** finestra di dialogo, fare clic su **Scarica File PUBLISH-SETTINGS**. Se non si è ancora connessi all'account Azure, sarà richiesta toolog in. Quindi verrà chiesto di file di impostazioni di pubblicazione toosave di Azure. (È possibile ignorare istruzioni di hello risultanti visualizzate nelle pagine di accesso hello - sono forniti dal portale di Azure hello e sono destinate agli utenti di Visual Studio.) Salvare il file tooyour di computer locale.

3. Ancora in hello **Importa informazioni sottoscrizione** finestra di dialogo, fare clic su hello **Sfoglia** pulsante, hello seleziona pubblicare file di impostazioni che è stato salvato in locale in precedenza e quindi fare clic su **aprire**.

4. Fare clic su **OK** tooclose hello **Importa informazioni sottoscrizione** finestra di dialogo.

## <a name="toocreate-a-new-storage-account"></a>toocreate un nuovo account di archiviazione
1. All'interno di hello **gli account di archiviazione** finestra di dialogo, fare clic su **Aggiungi**.

2. All'interno di hello **Add Storage Account** finestra di dialogo, fare clic su **New**.

3. All'interno di hello **nuovo Account di archiviazione** finestra di dialogo, specificare i valori per l'esempio hello:

   * Nome dell'account di archiviazione.

   * Posizione dell'account di archiviazione hello.

   * Descrizione dell'account di archiviazione hello.

   * account di archiviazione di Hello sottoscrizione toowhich hello appartiene.

4. Fare clic su **OK** tooclose hello **nuovo Account di archiviazione** finestra di dialogo.

Potrebbe richiedere alcuni minuti per il toobe di account di archiviazione creato. Dopo averlo creato, fare clic su **OK** tooclose hello **Add Storage Account** finestra di dialogo e il nuovo account di archiviazione verrà aggiunto toohello elenco di account di archiviazione disponibile.

## <a name="tooadd-an-existing-storage-account-toohello-list"></a>tooadd un elenco di toohello account di archiviazione esistente
1. Se non hai già una risorsa di archiviazione Azure account, crearlo hello passaggi elencati in hello **toocreate una nuova sezione di account di archiviazione** sopra. (In alternativa, è possibile creare un nuovo account di archiviazione in hello [il portale di gestione di Azure][Azure Management Portal].)

2. All'interno di hello **gli account di archiviazione** finestra di dialogo, fare clic su **Aggiungi**.

3. All'interno di hello **Add Storage Account** finestra di dialogo, immettere i valori per **nome** e **tasto**. chiave di accesso e sul nome di account Hello deve essere di un account di archiviazione di Azure esistente. Hello utilizzare **archiviazione** sezione di hello [il portale di gestione di Azure] [ Azure Management Portal] tooview nomi account di archiviazione e delle chiavi. Il **Add Storage Account** finestra di dialogo avrà un aspetto simile toohello seguente.
   
   ![][ic719497]

4. Fare clic su **OK** tooclose hello **Add Storage Account** finestra di dialogo.

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a>toomodify un toouse di account di archiviazione nuova chiave di accesso
1. All'interno di hello **gli account di archiviazione** finestra di dialogo, fare clic su account di archiviazione hello che desidera tooedit e quindi fare clic su **modifica**.

2. All'interno di hello **Edit Storage Account Access Key** finestra di dialogo, modificare hello **chiave di accesso** valore.

3. Fare clic su **OK** tooclose hello **Edit Storage Account Access Key** finestra di dialogo.

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a>tooremove un account di archiviazione dall'elenco di hello gestito in Eclipse
1. All'interno di hello **gli account di archiviazione** finestra di dialogo, fare clic su account di archiviazione hello che desidera tooedit e quindi fare clic su **rimuovere**.

2. Fare clic su **OK** quando richiesta tooremove hello account di archiviazione.

> [!NOTE]
> Rimozione di account di archiviazione hello tramite hello **gli account di archiviazione** finestra di dialogo verrà rimosso solo dall'elenco di hello degli account di archiviazione visualizzabile in Eclipse. Non rimuove account di archiviazione hello dalla sottoscrizione di Azure. Inoltre, account di archiviazione hello venga visualizzato nuovamente nell'elenco dopo che Eclipse ricarica i dettagli di hello della sottoscrizione.
> 
> 

## <a name="see-also"></a>Vedere anche
[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]

[L'installazione di hello Azure Toolkit per Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Creare un'applicazione Hello World per Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
