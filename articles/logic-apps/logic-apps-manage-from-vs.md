---
title: aaaManage logica App in Visual Studio - App Azure per la logica | Documenti Microsoft
description: Gestire le app per la logica e altri asset di Azure con Visual Studio Cloud Explorer
author: klam
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 12/19/2016
ms.author: LADocs; klam
ms.openlocfilehash: 419f83eb062b56e4ac2642dea4de1a025f747521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a>Gestire le app per la logica con Visual Studio Cloud Explorer

Sebbene hello [portale di Azure](https://portal.azure.com/) offre un modo eccellente per si toodesign e gestire le app di logica di Azure, è possibile utilizzare Visual Studio Cloud Explorer per la gestione di numerose risorse di Azure, incluse le app di logica. Visual Studio Cloud Explorer consente di esplorare, gestire, modificare e scaricare app per la logica pubblicate. Le attività di gestione includono l'abilitazione, la disabilitazione e la visualizzazione della cronologia delle esecuzioni. 

Prima di poter accedere alle app per la logica e gestirle in Visual Studio, installare e configurare questi strumenti di Visual Studio per App per la logica di Azure. 

## <a name="prerequisites"></a>Prerequisiti

* [Visual Studio 2015 o Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* [Versione più recente di Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 o versione successiva)
* [Visual Studio Cloud Explorer](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* Web toohello Access quando si utilizza Progettazione incorporato hello

## <a name="install-visual-studio-tools-for-logic-apps"></a>Installare gli strumenti di Visual Studio per le app per la logica

Dopo aver installato i prerequisiti di hello, scaricare e installare hello Azure logica App Tools per Visual Studio.

1. Aprire Visual Studio. In hello **strumenti** dal menu **estensioni e aggiornamenti**.
2. Espandere hello **Online** categoria, eseguire la ricerca online in hello Visual Studio Gallery.
3. Sfogliare o cercare **App per la logica** per visualizzare **Azure Logic Apps Tools for Visual Studio** (Strumenti per app per la logica di Azure per Visual Studio).
4. toodownload e l'estensione di hello installazione, fare clic su **scaricare**.
5. Al termine dell'installazione riavviare Visual Studio.

> [!NOTE]
> hello toodownload Azure logica App Tools per Visual Studio passare direttamente, toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).

## <a name="browse-for-logic-apps-in-cloud-explorer"></a>Cercare App per la logica in Cloud Explorer

1.  tooopen Cloud Explorer, in hello **vista** menu, scegliere **Cloud Explorer**.
2.  Cercare l'app per la logica, in base al gruppo di risorse o al tipo di risorsa. 

    * Se si passa dal tipo di risorsa, selezionare la sottoscrizione di Azure, espandere hello **logica app** sezione e selezionare l'app logica. 
    * Se si passa dal gruppo di risorse, espandere gruppo di risorse hello con l'app per la logica e selezionare l'app logica.

    tooview comandi per l'app di logica, fare doppio clic su app logica, o nella parte inferiore di hello del Cloud Explorer, scegliere hello **azioni** menu.

    ![Cercare l'app per la logica](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a>Modificare l'app per la logica con Progettazione app per la logica

In Cloud Explorer, è possibile aprire un'app logica attualmente distribuito in hello stessa finestra di progettazione utilizzati in hello portale di Azure. 

* tooedit app logica, in Cloud Explorer, l'app per la logica e scegliere **aperto con la logica App Editor**. 

* toopublish il toohello aggiornamenti cloud, scegliere **pubblica**. 

* Scegliere una nuova esecuzione toostart **eseguire Trigger**.

![Progettazione app per la logica](./media/logic-apps-manage-from-vs/designer.png)

Da Progettazione hello, è anche possibile **scaricare** un'app di logica. Questa azione automaticamente Parametrizza definizione dell'app logica hello e Salva definizione hello come un modello di distribuzione Azure Resource Manager. È possibile aggiungere questo progetto di distribuzione modello tooyour il gruppo di risorse di Azure.

## <a name="browse-your-logic-app-run-history"></a>Esplorare la cronologia di esecuzione dell'app per la logica

hello tooview cronologia per l'app, la logica di esecuzione delle app logica e scegliere **cronologia di esecuzione aprire**. tooreorder alla cronologia di esecuzione basato su qualsiasi intestazione di colonna hello indicato, selezionare proprietà hello.

![Cronologia di esecuzione](media/logic-apps-manage-from-vs/runs.png)

hello tooshow cronologia per un'istanza di esecuzione, pertanto è possibile esaminare i risultati, comprese hello input e output di ogni passaggio, eseguire hello fare doppio clic su uno dei hello eseguire istanze.

![Risultati della cronologia di esecuzione, input e output dei passaggi](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a>Passaggi successivi

* [Creare la prima app per la logica](logic-apps-create-a-logic-app.md)
* [Progettare, compilare e distribuire app per la logica in Visual Studio](logic-apps-deploy-from-vs.md)
* [Visualizzare esempi e scenari comuni](logic-apps-examples-and-scenarios.md)
* [Video: Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694) (Automatizzare i processi aziendali con App per la logica di Azure)
* [Video: Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462) (Integrare i sistemi con App per la logica di Azure)
