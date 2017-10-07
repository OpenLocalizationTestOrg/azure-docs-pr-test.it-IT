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
# <a name="manage-your-logic-apps-with-visual-studio-cloud-explorer"></a><span data-ttu-id="f5fb7-103">Gestire le app per la logica con Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="f5fb7-103">Manage your logic apps with Visual Studio Cloud Explorer</span></span>

<span data-ttu-id="f5fb7-104">Sebbene hello [portale di Azure](https://portal.azure.com/) offre un modo eccellente per si toodesign e gestire le app di logica di Azure, è possibile utilizzare Visual Studio Cloud Explorer per la gestione di numerose risorse di Azure, incluse le app di logica.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toodesign and manage Azure Logic Apps, you can use Visual Studio Cloud Explorer for managing many Azure assets, including logic apps.</span></span> <span data-ttu-id="f5fb7-105">Visual Studio Cloud Explorer consente di esplorare, gestire, modificare e scaricare app per la logica pubblicate.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-105">Visual Studio Cloud Explorer lets you browse, manage, edit, and download published logic apps.</span></span> <span data-ttu-id="f5fb7-106">Le attività di gestione includono l'abilitazione, la disabilitazione e la visualizzazione della cronologia delle esecuzioni.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-106">Management tasks include enable, disable, and view run history.</span></span> 

<span data-ttu-id="f5fb7-107">Prima di poter accedere alle app per la logica e gestirle in Visual Studio, installare e configurare questi strumenti di Visual Studio per App per la logica di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-107">Before you can access and manage your logic apps in Visual Studio, install and configure these Visual Studio tools for Azure Logic Apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f5fb7-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f5fb7-108">Prerequisites</span></span>

* [<span data-ttu-id="f5fb7-109">Visual Studio 2015 o Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f5fb7-109">Visual Studio 2015 or Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="f5fb7-110">[Versione più recente di Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="f5fb7-110">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="f5fb7-111">Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="f5fb7-111">Visual Studio Cloud Explorer</span></span>](https://marketplace.visualstudio.com/items?itemName=MicrosoftCloudExplorer.CloudExplorerforVisualStudio2015)
* <span data-ttu-id="f5fb7-112">Web toohello Access quando si utilizza Progettazione incorporato hello</span><span class="sxs-lookup"><span data-stu-id="f5fb7-112">Access toohello web when using hello embedded designer</span></span>

## <a name="install-visual-studio-tools-for-logic-apps"></a><span data-ttu-id="f5fb7-113">Installare gli strumenti di Visual Studio per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="f5fb7-113">Install Visual Studio tools for Logic Apps</span></span>

<span data-ttu-id="f5fb7-114">Dopo aver installato i prerequisiti di hello, scaricare e installare hello Azure logica App Tools per Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-114">After you install hello prerequisites, download and install hello Azure Logic Apps Tools for Visual Studio.</span></span>

1. <span data-ttu-id="f5fb7-115">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-115">Open Visual Studio.</span></span> <span data-ttu-id="f5fb7-116">In hello **strumenti** dal menu **estensioni e aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-116">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="f5fb7-117">Espandere hello **Online** categoria, eseguire la ricerca online in hello Visual Studio Gallery.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-117">Expand hello **Online** category so you can search online in hello Visual Studio Gallery.</span></span>
3. <span data-ttu-id="f5fb7-118">Sfogliare o cercare **App per la logica** per visualizzare **Azure Logic Apps Tools for Visual Studio** (Strumenti per app per la logica di Azure per Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="f5fb7-118">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="f5fb7-119">toodownload e l'estensione di hello installazione, fare clic su **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-119">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="f5fb7-120">Al termine dell'installazione riavviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-120">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="f5fb7-121">hello toodownload Azure logica App Tools per Visual Studio passare direttamente, toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span><span class="sxs-lookup"><span data-stu-id="f5fb7-121">toodownload hello Azure Logic Apps Tools for Visual Studio directly, go toohello [Visual Studio Marketplace](https://visualstudiogallery.msdn.microsoft.com/e25ad307-46cf-412e-8ba5-5b555d53d2d9).</span></span>

## <a name="browse-for-logic-apps-in-cloud-explorer"></a><span data-ttu-id="f5fb7-122">Cercare App per la logica in Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="f5fb7-122">Browse for logic apps in Cloud Explorer</span></span>

1.  <span data-ttu-id="f5fb7-123">tooopen Cloud Explorer, in hello **vista** menu, scegliere **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-123">tooopen Cloud Explorer, on hello **View** menu, choose **Cloud Explorer**.</span></span>
2.  <span data-ttu-id="f5fb7-124">Cercare l'app per la logica, in base al gruppo di risorse o al tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-124">Browse for your logic app, either by resource group or by resource type.</span></span> 

    * <span data-ttu-id="f5fb7-125">Se si passa dal tipo di risorsa, selezionare la sottoscrizione di Azure, espandere hello **logica app** sezione e selezionare l'app logica.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-125">If you browse by resource type, select your Azure subscription, expand hello **Logic Apps** section, and select your logic app.</span></span> 
    * <span data-ttu-id="f5fb7-126">Se si passa dal gruppo di risorse, espandere gruppo di risorse hello con l'app per la logica e selezionare l'app logica.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-126">If you browse by resource group, expand hello resource group that has your logic app, and select your logic app.</span></span>

    <span data-ttu-id="f5fb7-127">tooview comandi per l'app di logica, fare doppio clic su app logica, o nella parte inferiore di hello del Cloud Explorer, scegliere hello **azioni** menu.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-127">tooview commands for your logic app, either right-click your logic app, or at hello bottom of Cloud Explorer, choose from hello **Actions** menu.</span></span>

    ![Cercare l'app per la logica](./media/logic-apps-manage-from-vs/browse.png)

## <a name="edit-your-logic-app-with-logic-apps-designer"></a><span data-ttu-id="f5fb7-129">Modificare l'app per la logica con Progettazione app per la logica</span><span class="sxs-lookup"><span data-stu-id="f5fb7-129">Edit your logic app with Logic Apps Designer</span></span>

<span data-ttu-id="f5fb7-130">In Cloud Explorer, è possibile aprire un'app logica attualmente distribuito in hello stessa finestra di progettazione utilizzati in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-130">From Cloud Explorer, you can open a currently deployed logic app in hello same designer that you use in hello Azure portal.</span></span> 

* <span data-ttu-id="f5fb7-131">tooedit app logica, in Cloud Explorer, l'app per la logica e scegliere **aperto con la logica App Editor**.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-131">tooedit your logic app, in Cloud Explorer, right-click your logic app, and select **Open with Logic App Editor**.</span></span> 

* <span data-ttu-id="f5fb7-132">toopublish il toohello aggiornamenti cloud, scegliere **pubblica**.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-132">toopublish your updates toohello cloud, choose **Publish**.</span></span> 

* <span data-ttu-id="f5fb7-133">Scegliere una nuova esecuzione toostart **eseguire Trigger**.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-133">toostart a new run, choose **Run Trigger**.</span></span>

![Progettazione app per la logica](./media/logic-apps-manage-from-vs/designer.png)

<span data-ttu-id="f5fb7-135">Da Progettazione hello, è anche possibile **scaricare** un'app di logica.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-135">From hello designer, you can also **Download** a logic app.</span></span> <span data-ttu-id="f5fb7-136">Questa azione automaticamente Parametrizza definizione dell'app logica hello e Salva definizione hello come un modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-136">This action automatically parameterizes hello logic app definition, and saves hello definition as an Azure Resource Manager deployment template.</span></span> <span data-ttu-id="f5fb7-137">È possibile aggiungere questo progetto di distribuzione modello tooyour il gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-137">You can add this deployment template tooyour Azure Resource Group project.</span></span>

## <a name="browse-your-logic-app-run-history"></a><span data-ttu-id="f5fb7-138">Esplorare la cronologia di esecuzione dell'app per la logica</span><span class="sxs-lookup"><span data-stu-id="f5fb7-138">Browse your logic app run history</span></span>

<span data-ttu-id="f5fb7-139">hello tooview cronologia per l'app, la logica di esecuzione delle app logica e scegliere **cronologia di esecuzione aprire**.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-139">tooview hello run history for your logic app, right-click your logic app, and select **Open run history**.</span></span> <span data-ttu-id="f5fb7-140">tooreorder alla cronologia di esecuzione basato su qualsiasi intestazione di colonna hello indicato, selezionare proprietà hello.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-140">tooreorder your run history based on any of hello properties shown, select hello column header.</span></span>

![Cronologia di esecuzione](media/logic-apps-manage-from-vs/runs.png)

<span data-ttu-id="f5fb7-142">hello tooshow cronologia per un'istanza di esecuzione, pertanto è possibile esaminare i risultati, comprese hello input e output di ogni passaggio, eseguire hello fare doppio clic su uno dei hello eseguire istanze.</span><span class="sxs-lookup"><span data-stu-id="f5fb7-142">tooshow hello run history for an instance so you can review hello run results, including hello inputs and outputs from each step, double-click one of hello run instances.</span></span>

![Risultati della cronologia di esecuzione, input e output dei passaggi](./media/logic-apps-manage-from-vs/history.png)

## <a name="next-steps"></a><span data-ttu-id="f5fb7-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5fb7-144">Next steps</span></span>

* [<span data-ttu-id="f5fb7-145">Creare la prima app per la logica</span><span class="sxs-lookup"><span data-stu-id="f5fb7-145">Create your first logic app</span></span>](logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="f5fb7-146">Progettare, compilare e distribuire app per la logica in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f5fb7-146">Design, build, and deploy logic apps in Visual Studio</span></span>](logic-apps-deploy-from-vs.md)
* [<span data-ttu-id="f5fb7-147">Visualizzare esempi e scenari comuni</span><span class="sxs-lookup"><span data-stu-id="f5fb7-147">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* <span data-ttu-id="f5fb7-148">[Video: Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694) (Automatizzare i processi aziendali con App per la logica di Azure)</span><span class="sxs-lookup"><span data-stu-id="f5fb7-148">[Video: Automate business processes with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/T694)</span></span>
* <span data-ttu-id="f5fb7-149">[Video: Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462) (Integrare i sistemi con App per la logica di Azure)</span><span class="sxs-lookup"><span data-stu-id="f5fb7-149">[Video: Integrate your systems with Azure Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)</span></span>
