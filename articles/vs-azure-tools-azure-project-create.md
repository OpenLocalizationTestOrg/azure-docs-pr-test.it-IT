---
title: un progetto di servizio cloud di Azure con Visual Studio aaaCreating | Documenti Microsoft
description: Informazioni su ora toocreate un progetto di servizio cloud di Azure con Visual Studio
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Creazione di un progetto di servizio cloud di Azure con Visual Studio
Hello Azure Tools per Visual Studio fornisce un modello di progetto che consente di creare un servizio cloud di Azure. Dopo aver creato il progetto di hello, Visual Studio consente tooconfigure, eseguire il debug e distribuire tooAzure servizio cloud di hello.

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a>Passaggi toocreate un progetto di servizio cloud di Azure in Visual Studio
In questa sezione viene illustrata la creazione di un progetto di servizio cloud di Azure in Visual Studio con uno o più ruoli Web.  

1. Avviare Visual Studio come amministratore.

1. Scegliere dal menu principale hello **File** > **New** > **progetto**.

1. Selezionare **Cloud** da hello Visual c# o Visual Basic i nodi di modello di progetto e selezionare **servizio Cloud di Azure** elenco hello di modelli.

    ![Nuovo servizio cloud di Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Specificare la versione di hello .NET Framework si desidera toouse toodevelop il progetto.

1. Immettere un nome e percorso per il progetto e un nome per la soluzione hello. 

1. Selezionare **OK**.

1. In hello **nuovo servizio Cloud di Microsoft Azure** finestra di dialogo, i ruoli selezionare hello che si desidera tooadd e scegliere tooadd pulsante freccia destra di hello li tooyour soluzione.

    ![Selezionare i ruoli del nuovo servizio cloud di Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. un ruolo che si è aggiunto, al passaggio del mouse sul ruolo hello in hello toorename **nuovo servizio Cloud di Microsoft Azure** finestra di dialogo, selezionare il menu di scelta rapida hello **rinominare**. È inoltre possibile rinominare un ruolo all'interno della soluzione (in hello **Esplora**) dopo che è stato aggiunto.

    ![Rinominare un ruolo dei servizi cloud di Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

progetto di Visual Studio Azure Hello dispone di associazioni toohello ruolo progetti nella soluzione hello. progetto Hello include anche hello *file di definizione del servizio* e *file di configurazione del servizio*:

- **File di definizione del servizio** -definisce le impostazioni di runtime hello per l'applicazione, inclusi i ruoli sono necessari, endpoint e dimensioni della macchina virtuale. 
- **File di configurazione del servizio** -consente di configurare il numero di istanze di un ruolo viene eseguito e hello valori delle impostazioni di hello è definite per un ruolo. 

Per ulteriori informazioni su questi file, vedere [configurare i ruoli di hello per un servizio cloud di Azure con Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Passaggi successivi
- [Gestione dei ruoli nei progetti di servizi cloud di Azure con Visual Studio](./vs-azure-tools-cloud-service-project-managing-roles.md)
