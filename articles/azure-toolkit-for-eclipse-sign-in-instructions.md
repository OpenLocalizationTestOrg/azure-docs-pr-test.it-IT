---
title: aaaSign In istruzioni per hello Azure Toolkit per Eclipse | Documenti Microsoft
description: Informazioni su come toosign in Microsoft Azure tramite hello Azure Toolkit per Eclipse.
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
ms.openlocfilehash: 95be64750ca0147f76dae8f364fad80cb9ccc969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sign-in-instructions-for-hello-azure-toolkit-for-eclipse"></a>Azure Sign In istruzioni per hello Azure Toolkit per Eclipse

Hello Azure Toolkit per Eclipse fornisce due metodi per la firma nell'account di Azure:

  * **Interattivo**: le credenziali di Azure vengono immesse ogni volta che si accede all'account Azure.
  * **Automatizzata** : quando si utilizza questo metodo, si creerà un file di credenziali che contiene i dati dell'entità servizio, dopo il quale è possibile utilizzare hello credenziali file tooautomatically accesso all'account Azure.

Hello in hello le sezioni seguenti viene descritta la modalità toouse ogni metodo.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-interactively"></a>Accesso all'account Azure in modo interattivo

Hello passaggi seguenti verranno illustrato come toosign in Azure immettendo manualmente le credenziali di Azure.

1. Aprire il progetto con Eclipse.

1. Fare clic su **Tools** (Strumenti), su **Azure** e quindi fare clic su **Sign In** (Accedi).

   ![Menu di Eclipse per l'accesso ad Azure][I01]

1. Quando hello **Azure Accedi** viene visualizzata la finestra di dialogo, selezionare **Interactive**, quindi fare clic su **Accedi**.

   ![Finestra di dialogo di accesso][I02]

1. Quando hello **Log di Azure** la finestra di dialogo visualizzata, immettere le credenziali di Azure e quindi fare clic su **Accedi**.

   ![Finestra di dialogo di accesso ad Azure][I03]

1. Quando hello **sottoscrizioni selezionare** viene visualizzata la finestra di dialogo, le sottoscrizioni selezionare hello che desidera toouse e quindi fare clic su **OK**.

   ![Finestra di dialogo Seleziona sottoscrizioni][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a>Disconnessione dell'account di Azure quando l'accesso è stato eseguito in modo interattivo

Dopo aver configurato i passaggi di hello nella sezione precedente di hello, verrà disconnesso automaticamente all'account Azure a ogni avvio di Eclipse. Tuttavia, se si desidera toosign senza accesso all'account di Azure senza dover riavviare Eclipse, utilizzare hello alla procedura seguente.

1. In Eclipse fare clic su **Tools** (Strumenti), su **Azure** e quindi su **Sign Out** (Disconnetti).

   ![Menu di Eclipse per la disconnessione da Azure][L01]

1. Quando hello **Azure Sign Out** viene visualizzata la finestra di dialogo, fare clic su **Sì**.

   ![Finestra di dialogo di disconnessione][L02]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-toouse-in-hello-future"></a>Firma automaticamente all'account Azure e la creazione di credenziali di un file toouse in hello future

Hello passaggi seguenti verranno illustrati la creazione di un file di credenziali che contiene i dati dell'entità servizio. Dopo aver completato questi passaggi, sarà Eclipse automaticamente si in Azure ogni volta che si usa hello credenziali file tooautomatically sign aprire il progetto.

1. Aprire il progetto con Eclipse.

1. Fare clic su **Tools** (Strumenti), su **Azure** e quindi fare clic su **Sign In** (Accedi).

   ![Menu di Eclipse per l'accesso ad Azure][A01]

1. Quando hello **Azure Accedi** viene visualizzata la finestra di dialogo, selezionare **automatizzata**, quindi fare clic su **New**.

   ![Finestra di dialogo di accesso][A02]

1. Quando hello **Log di Azure** la finestra di dialogo visualizzata, immettere le credenziali di Azure e quindi fare clic su **Accedi**.

   ![Finestra di dialogo di accesso ad Azure][A03]

1. Quando hello **creare file di autenticazione** viene visualizzata la finestra di dialogo, le sottoscrizioni selezionare hello desidera toouse, scegliere la directory di destinazione e quindi fare clic su **avviare**.

   ![Finestra di dialogo di accesso ad Azure][A04]

1. Hello **dell'entità servizio Creatation stato** verrà visualizzata la finestra di dialogo, dopo che sono stati creati i file, fare clic su **OK**.

   ![Finestra di dialogo Stato creazione entità servizio][A05]

1. Quando hello **Azure Accedi** viene visualizzata la finestra di dialogo, fare clic su **Accedi**.

   ![Finestra di dialogo di accesso ad Azure][A06]

1. Quando hello **sottoscrizioni selezionare** viene visualizzata la finestra di dialogo, le sottoscrizioni selezionare hello che desidera toouse e quindi fare clic su **OK**.

   ![Finestra di dialogo Seleziona sottoscrizioni][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a>Disconnessione dell'account Azure quando l'accesso è stato eseguito in modo automatico

Dopo aver configurato i passaggi di hello nella sezione precedente di hello, hello Azure Toolkit comporta l'accesso automatico all'account Azure a ogni avvio di Eclipse. Tuttavia, toosign dell'account di Azure e di impedire l'accesso automatico, utilizzare hello, alla procedura seguente hello Azure Toolkit.

1. In Eclipse fare clic su **Tools** (Strumenti), su **Azure** e quindi su **Sign Out** (Disconnetti).

   ![Menu di Eclipse per la disconnessione da Azure][L01]

1. Quando hello **Azure Sign Out** viene visualizzata la finestra di dialogo, fare clic su **Sì**.

   ![Finestra di dialogo di disconnessione][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a>Accesso automatico all'account Azure usando un file di credenziali già creato

Se si accede all'esterno di Azure quando si usa Eclipse, è necessario tooreconfigure hello Azure Toolkit per Eclipse toouse un file di credenziali che è stato creato prima di poter firmare automaticamente nell'account di Azure. Hello passaggi seguenti verranno illustrati configurazione hello Azure Toolkit toouse un file di credenziali esistente.

1. Aprire il progetto con Eclipse.

1. Fare clic su **Tools** (Strumenti), su **Azure** e quindi fare clic su **Sign In** (Accedi).

   ![Menu di Eclipse per l'accesso ad Azure][A01]

1. Quando hello **Azure Accedi** viene visualizzata la finestra di dialogo, selezionare **automatizzata**, quindi fare clic su **Sfoglia**.

   ![Finestra di dialogo di accesso][A02]

1. Quando hello **selezionare File autenticato** viene visualizzata la finestra di dialogo, selezionare un file di credenziali creato in precedenza e quindi fare clic su **selezionare**.

   ![Finestra di dialogo di accesso][A08]

1. Quando hello **Azure Accedi** viene visualizzata la finestra di dialogo, fare clic su **Accedi**.

   ![Finestra di dialogo di accesso ad Azure][A06]

1. Quando hello **sottoscrizioni selezionare** viene visualizzata la finestra di dialogo, le sottoscrizioni selezionare hello che desidera toouse e quindi fare clic su **OK**.

   ![Finestra di dialogo Seleziona sottoscrizioni][A07]

## <a name="see-also"></a>Vedere anche
Per ulteriori informazioni su hello Azure Toolkit per ambienti Java, vedere hello seguenti collegamenti:

* [Toolkit di Azure per Eclipse]
  * [Novità in Azure Toolkit per Eclipse hello]
  * [L'installazione di hello Azure Toolkit per Eclipse]
  * *Sign In istruzioni per hello Azure Toolkit for Eclipse (articolo)*
  * [Creare un'app Web Hello World per Azure in Eclipse]
* [Toolkit di Azure per IntelliJ]
  * [Novità in Azure Toolkit per IntelliJ hello]
  * [Installazione di hello Azure Toolkit per IntelliJ]
  * [Sign In istruzioni per hello Azure Toolkit per IntelliJ]
  * [Creare un'App Web Hello World per Azure in IntelliJ]

Per ulteriori informazioni sull'uso di Azure con Java, vedere hello [Centro per sviluppatori Java di Azure] hello e [Java Tools per Visual Studio Team Services].

<!-- URL List -->

[Toolkit di Azure per Eclipse]: ./azure-toolkit-for-eclipse.md
[Toolkit di Azure per IntelliJ]: ./azure-toolkit-for-intellij.md
[Creare un'app Web Hello World per Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Creare un'App Web Hello World per Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[L'installazione di hello Azure Toolkit per Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Installazione di hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Sign In Instructions for hello Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Sign In istruzioni per hello Azure Toolkit per IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Novità in Azure Toolkit per Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Novità in Azure Toolkit per IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[Centro per sviluppatori Java di Azure]: https://azure.microsoft.com/develop/java/
[Java Tools per Visual Studio Team Services]: https://java.visualstudio.com/

<!-- IMG List -->

[I01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: ./media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
