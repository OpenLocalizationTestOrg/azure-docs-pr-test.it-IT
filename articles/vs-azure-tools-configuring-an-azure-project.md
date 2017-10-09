---
title: un progetto di servizio cloud di Azure con Visual Studio aaaConfigure | Documenti Microsoft
description: Informazioni di progetto di servizio in Visual Studio, a seconda dei requisiti per il progetto cloud tooconfigure di Azure.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>Configurare un progetto di servizio cloud di Azure con Visual Studio
È possibile configurare un progetto di servizio cloud di Azure, in base ai requisiti specifici per il progetto. È possibile impostare proprietà per il progetto di hello per hello seguenti categorie:

- **Pubblicare un tooAzure servizio cloud** -è possibile impostare una proprietà toomake assicurarsi che un servizio distribuito tooAzure di esistente cloud non è stato eliminato accidentalmente.
- **Eseguire o eseguire il debug di un servizio cloud nel computer locale hello** -è possibile selezionare un toouse di configurazione del servizio e indicare se si desidera toostart hello emulatore di archiviazione Azure.
- **Convalidare un pacchetto del servizio cloud al momento della creazione** -è possibile decidere tootreat gli avvisi come errori, in modo che è possibile verificare il pacchetto del servizio cloud hello distribuisce senza problemi. 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a>Passaggi tooconfigure un progetto di servizio cloud di Azure
1. Aprire o creare un progetto di servizio cloud in Visual Studio

1. In **Esplora**, fare clic sul progetto hello e selezionare il menu di scelta rapida hello **proprietà**.
   
1. Nella pagina delle proprietà del progetto hello, selezionare hello **sviluppo** scheda.

    ![Menu Proprietà del progetto](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. Impostare **Chiedi conferma prima di eliminare una distribuzione esistente** troppo**True**. Questa impostazione consente di tooensure non è stato eliminato accidentalmente una distribuzione esistente in Azure

1. Seleziona hello desiderato **configurazione del servizio** tooindicate la configurazione di servizio desiderato toouse quando si esegue o eseguire il debug del servizio cloud localmente. Per ulteriori informazioni su come toomodify una configurazione del servizio per un ruolo, vedere [come tooconfigure hello ruoli per un Azure cloud del servizio con Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).

1. Impostare **emulatore di archiviazione Azure avvia** troppo**True** toostart hello emulatore di archiviazione Azure quando si esegue o eseguire il debug del servizio cloud localmente.

1. Impostare **considerarli come errori** troppo**True** toomake che non è possibile pubblicare se sono presenti errori di convalida del pacchetto.

1. Impostare **utilizzare porte del progetto web** troppo**True** toomake assicurarsi che il ruolo web Usa hello stessa porta ogni volta che viene avviato in locale in IIS Express.

1. Barra degli strumenti di Visual Studio hello, selezionare **salvare**.

## <a name="next-steps"></a>Passaggi successivi
- [Configurare un progetto di servizio cloud di Azure tramite più configurazioni del servizio](vs-azure-tools-multiple-services-project-configurations.md)

