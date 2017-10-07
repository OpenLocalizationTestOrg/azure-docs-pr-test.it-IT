---
title: aaaSign-nelle istruzioni per hello Azure Toolkit per IntelliJ | Documenti Microsoft
description: Informazioni su come toosign in tooMicrosoft Azure tramite hello Azure Toolkit per IntelliJ.
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
ms.openlocfilehash: 2de781fc19267cce133b1e6456481497e165fce4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-instructions-for-hello-azure-toolkit-for-intellij"></a>Accesso le istruzioni per hello Azure Toolkit per IntelliJ

Hello Azure Toolkit per IntelliJ fornisce due metodi per la firma in tooyour account di Azure:

  * **Interattivo**: immesso le credenziali di Azure ogni volta che si accede in tooyour account Azure.
  * **Automatizzata**: puoi creare un file di credenziali che è possibile utilizzare tooautomatically sign in tooyour account Azure.

Hello sezioni seguenti descrivono come toouse ogni metodo.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-tooyour-azure-account-interactively"></a>Accedi tooyour account Azure in modo interattivo

toosign in tooAzure immettendo manualmente le credenziali di Azure, hello seguenti:

1. Aprire il progetto con IntelliJ IDEA.

2. Fare clic su **strumenti**, punto troppo**Azure**, quindi fare clic su **Azure Accedi**.

   ![comando IntelliJ Azure Accedi Hello][I01]

3. In hello **Azure Accedi** selezionare **Interactive**, quindi fare clic su **Accedi**.

   ![Hello Azure Accedi finestra con Interactive selezionato][I02]

4. In hello **Log di Azure** la finestra di dialogo visualizzata, immettere le credenziali di Azure e quindi fare clic su **Accedi**.

   ![finestra di dialogo di accesso di Azure Hello][I03]

5. In hello **sottoscrizioni selezionare** la finestra di dialogo, le sottoscrizioni selezionare hello che desidera toouse e quindi fare clic su **OK**.

   ![la finestra di dialogo selezionare le sottoscrizioni di Hello][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a>Disconnettersi dall'account di Azure dopo che l'accesso è stato eseguito in modo interattivo

Dopo aver configurato l'account utilizzando hello passaggi precedenti, verrà automaticamente disconnesso all'account Azure ogni volta che si riavvia IntelliJ IDEA. Tuttavia, se si desidera toosign senza accesso all'account Azure *senza* riavvio IntelliJ IDEA, hello seguente.

1. In IntelliJ IDEA, su hello **strumenti** menu, scegliere troppo**Azure**e quindi fare clic su **Azure Sign Out**.

   ![comando IntelliJ Azure Disconnetti Hello][L01]

2. In hello **Azure Sign Out** finestra di conferma, fare clic su **Sì**.

   ![finestra Hello Azure Sign Out conferma][L02]

## <a name="sign-in-tooyour-azure-account-automatically"></a>Accedi automaticamente tooyour account Azure

La sezione seguente illustra come creare un file di credenziali che contiene i dati dell'entità servizio. Dopo aver completato questo processo, Eclipse utilizza hello credenziali file tooautomatically sign in tooAzure ogni volta che si aprire il progetto.

1. Aprire il progetto con IntelliJ IDEA.

2. In hello **strumenti** menu, scegliere troppo**Azure**e quindi fare clic su **Azure Accedi**.

   ![comando IntelliJ Azure Accedi Hello][A01]

3. In hello **Azure Accedi** selezionare **automatizzata**e quindi fare clic su **New**.

   ![Hello Azure Accedi finestra con automatizzati selezionata][A02]

4. In hello **finestra di dialogo account di accesso Azure** finestra, immettere le credenziali di Azure e quindi fare clic su **Accedi**.

   ![finestra di dialogo di accesso di Azure Hello][A03]

5. In hello **creare un file di autenticazione** (finestra), le sottoscrizioni selezionare hello desidera toouse, scegliere la directory di destinazione e quindi fare clic su **avviare**.

   ![finestra di creare file di autenticazione Hello][A04]

6. In hello **lo stato di creazione dell'entità servizio** nella finestra di dialogo dopo i file sono stati creati correttamente, fare clic su **OK**.

   ![Hello nella finestra di dialogo dello stato di creazione dell'entità servizio][A05]

7. In hello **Azure Accedi** finestra, fare clic su **Accedi**.

   ![Finestra di dialogo di accesso ad Azure][A06]

8. In hello **sottoscrizioni selezionare** la finestra di dialogo, le sottoscrizioni selezionare hello che desidera toouse e quindi fare clic su **OK**.

   ![la finestra di dialogo selezionare le sottoscrizioni di Hello][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a>Disconnettersi dall'account di Azure dopo che l'accesso è stato in modo automatico

Dopo aver configurato l'account utilizzando hello passaggi precedenti, hello Azure Toolkit si accede automaticamente tooyour account Azure ogni volta che si riavvia IntelliJ IDEA. Tuttavia, toosign dell'account di Azure e di evitare hello Azure Toolkit da l'accesso automatico, hello seguenti:

1. In IntelliJ IDEA, su hello **strumenti** menu, scegliere troppo**Azure**e quindi fare clic su **Azure Sign Out**.

   ![comando IntelliJ Azure Disconnetti Hello][L01]

2. In hello **Azure Sign Out** finestra di conferma, fare clic su **Sì**.

   ![finestra Hello Azure Sign Out conferma][L03]

## <a name="sign-in-tooyour-azure-account-automatically-by-using-an-existing-credentials-file"></a>Accedi tooyour account Azure automaticamente utilizzando un file di credenziali esistente

Se si accede senza accesso all'account Azure quando si utilizza IntelliJ IDEA, è necessario utilizzare un segno di tooautomatically file credenziali esistenti in toohello account. tooconfigure hello Azure Toolkit per Eclipse toouse un file di credenziali esistente, hello seguenti:

1. Aprire il progetto con IntelliJ IDEA.

2. In hello **strumenti** menu, scegliere troppo**Azure**e quindi fare clic su **Azure Accedi**.

   ![comando IntelliJ Azure Accedi Hello][A01]

3. In hello **Azure Accedi** selezionare **automatizzata**, quindi fare clic su **Sfoglia**.

   ![Hello Azure Accedi finestra con automatizzati selezionata][A02]

4. In hello **seleziona File di autenticazione** nella finestra di dialogo selezionare un file di credenziali creato in precedenza e quindi fare clic su **selezionare**.

   ![finestra di dialogo Seleziona File di autenticazione Hello][A08]

5. In hello **Azure Accedi** finestra, fare clic su **Accedi**.

   ![Hello Azure Accedi finestra con automatizzati selezionata][A06]

6. In hello **sottoscrizioni selezionare** la finestra di dialogo, le sottoscrizioni selezionare hello che desidera toouse e quindi fare clic su **OK**.

   ![la finestra di dialogo selezionare le sottoscrizioni di Hello][A07]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti collegamenti:

* [Toolkit di Azure per Eclipse]
  * [Novità di hello Azure Toolkit per Eclipse]
  * [L'installazione di hello Azure Toolkit per Eclipse]
  * [Istruzioni di accesso per hello Azure Toolkit per Eclipse]
  * [Creare un'app Web Hello World per Azure in Eclipse]
* [Toolkit di Azure per IntelliJ]
  * [Novità di hello Azure Toolkit per IntelliJ]
  * [Installazione di hello Azure Toolkit per IntelliJ]
  * *Accesso le istruzioni per hello Azure Toolkit per IntelliJ* (in questo articolo)
  * [Creare un'App Web Hello World per Azure in IntelliJ]

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md
[Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[L'installazione di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Istruzioni di accesso per hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign-in instructions for hello Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novità di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Novità di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
