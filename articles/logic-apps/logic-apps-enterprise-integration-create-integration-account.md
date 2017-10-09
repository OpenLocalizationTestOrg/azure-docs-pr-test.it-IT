---
title: aaaCreate, collegamento, eliminare o spostare un account di integrazione in App per la logica di Azure | Documenti Microsoft
description: Come toocreate un'integrazione account, quindi collegarlo tooyour logica App
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="2ea36-103">Cos'è un account di integrazione?</span><span class="sxs-lookup"><span data-stu-id="2ea36-103">What is an integration account?</span></span>

<span data-ttu-id="2ea36-104">Un account di integrazione consente enterprise integration App toomanage elementi, inclusi gli schemi, mappe, i certificati, partner e contratti.</span><span class="sxs-lookup"><span data-stu-id="2ea36-104">An integration account allows enterprise integration apps toomanage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="2ea36-105">Qualsiasi applicazione di integrazione che è creare Usa un tooaccess account integrazione questi schemi, mappe, i certificati e così via.</span><span class="sxs-lookup"><span data-stu-id="2ea36-105">Any integration app you create uses an integration account tooaccess these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="2ea36-106">Creare un account di integrazione</span><span class="sxs-lookup"><span data-stu-id="2ea36-106">Create an integration account</span></span>

1.  <span data-ttu-id="2ea36-107">Accedi toohello [portale di Azure](http://portal.azure.com "portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="2ea36-107">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="2ea36-108">Scegliere dal menu a sinistra hello **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-108">From hello left menu, select **More services**.</span></span>

    ![Selezionare "Altri servizi"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="2ea36-110">Nella casella di ricerca hello, digitare "integrazione" per il filtro.</span><span class="sxs-lookup"><span data-stu-id="2ea36-110">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="2ea36-111">Selezionare dall'elenco risultati hello **account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-111">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtro su "integrazione", selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="2ea36-113">Nella parte superiore di hello della pagina hello, scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-113">At hello top of hello page, choose **Add**.</span></span>

    ![Scegliere Aggiungi](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="2ea36-115">Denominare l'account di integrazione e la sottoscrizione di Azure che si desidera toouse di hello Seleziona.</span><span class="sxs-lookup"><span data-stu-id="2ea36-115">Name your integration account and select hello Azure subscription that you want toouse.</span></span> <span data-ttu-id="2ea36-116">È possibile creare un nuovo **Gruppo di risorse** o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="2ea36-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="2ea36-117">Selezionare quindi la **località** in cui eseguire l'hosting dell'account di integrazione e un **piano tariffario**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="2ea36-118">Al termine, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-118">When you're ready, choose **Create**.</span></span>

    ![Immettere i dettagli dell'account di integrazione](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="2ea36-120">Provisioning tramite Azure l'account di integrazione nel percorso selezionato hello, che deve essere completato entro 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="2ea36-120">Azure provisions your integration account  in hello selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="2ea36-121">Aggiornare la pagina hello.</span><span class="sxs-lookup"><span data-stu-id="2ea36-121">Refresh hello page.</span></span> <span data-ttu-id="2ea36-122">Il nuovo account di integrazione verrà visualizzato nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="2ea36-122">You see your new integration account listed.</span></span>

    ![Visualizzazione del nuovo account di integrazione](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="2ea36-124">Successivamente, creare collegamenti account integrazione hello è creato tooyour logica app.</span><span class="sxs-lookup"><span data-stu-id="2ea36-124">Next, link hello integration account that you created tooyour logic app.</span></span> 

## <a name="link-an-integration-account-tooa-logic-app"></a><span data-ttu-id="2ea36-125">Collegare un'applicazione di integrazione account tooa logica</span><span class="sxs-lookup"><span data-stu-id="2ea36-125">Link an integration account tooa logic app</span></span>

<span data-ttu-id="2ea36-126">toogive App per la logica di accesso toomaps, schemi, contratti e altri elementi nell'account di integrazione, collegamento hello integrazione account tooyour logica app.</span><span class="sxs-lookup"><span data-stu-id="2ea36-126">toogive your logic apps access toomaps, schemas, agreements, and other artifacts in your integration account, link hello integration account tooyour logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="2ea36-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2ea36-127">Prerequisites</span></span>

* <span data-ttu-id="2ea36-128">Un account di integrazione</span><span class="sxs-lookup"><span data-stu-id="2ea36-128">An integration account</span></span>
* <span data-ttu-id="2ea36-129">App per la logica</span><span class="sxs-lookup"><span data-stu-id="2ea36-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="2ea36-130">Verificare che l'applicazione di account e la logica di integrazione siano hello *nello stesso percorso Azure* prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="2ea36-130">Make sure your integration account and logic app are in hello *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="2ea36-131">Nel portale di Azure hello, selezionare l'app per la logica e controllare la posizione logica dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2ea36-131">In hello Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Selezionare l'app per la logica, controllare la località](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="2ea36-133">In **Impostazioni**, selezionare **Account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="2ea36-135">Da hello **selezionare un account di integrazione** elencare, account di integrazione hello selezionare desiderato toolink tooyour logica app.</span><span class="sxs-lookup"><span data-stu-id="2ea36-135">From hello **Select an Integration account** list, select hello integration account you want toolink tooyour logic app.</span></span> <span data-ttu-id="2ea36-136">Scegliere il collegamento, toofinish **salvare**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-136">toofinish linking, choose **Save**.</span></span>

    ![Selezionare l'account di integrazione](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="2ea36-138">Si riceve una notifica che mostra l'integrazione di account è collegato tooyour logica app e che tutti gli elementi nell'account di integrazione sono ora disponibili tooyour logica app.</span><span class="sxs-lookup"><span data-stu-id="2ea36-138">You get a notification that shows your integration account is linked tooyour logic app,  and that all artifacts in your integration account are now available tooyour logic app.</span></span>

    ![Logica app è collegata tooyour account di integrazione](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="2ea36-140">Ora che l'account di integrazione è collegato tooyour logica app, è possibile utilizzare i connettori di hello B2B nelle App logica.</span><span class="sxs-lookup"><span data-stu-id="2ea36-140">Now that your integration account is linked tooyour logic app, you can use hello B2B connectors in your logic apps.</span></span> <span data-ttu-id="2ea36-141">Alcuni connettori B2B comuni includono la convalida XML e la codifica e decodifica di file flat.</span><span class="sxs-lookup"><span data-stu-id="2ea36-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="2ea36-142">Eliminare l'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="2ea36-142">Delete your integration account</span></span>

1. <span data-ttu-id="2ea36-143">Selezionare **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-143">Select **More services**.</span></span>

    ![Selezionare "Altri servizi"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="2ea36-145">Nella casella di ricerca hello, digitare "integrazione" per il filtro.</span><span class="sxs-lookup"><span data-stu-id="2ea36-145">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="2ea36-146">Selezionare dall'elenco risultati hello **account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-146">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtro su "integrazione", selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="2ea36-148">Selezionare l'account di integrazione hello che si desidera toodelete.</span><span class="sxs-lookup"><span data-stu-id="2ea36-148">Select hello integration account that you want toodelete.</span></span>

    ![Selezionare toodelete account di integrazione](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="2ea36-150">Scegliere dal menu hello **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-150">On hello menu, choose **Delete**.</span></span>

    ![Scegliere "Elimina"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="2ea36-152">Confermare l'account di integrazione di hello toodelete scelte.</span><span class="sxs-lookup"><span data-stu-id="2ea36-152">Confirm your choice toodelete hello integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="2ea36-153">Spostare l'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="2ea36-153">Move your integration account</span></span>

<span data-ttu-id="2ea36-154">toomove un tooanother account integrazione gruppo sottoscrizione o la risorsa di Azure, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="2ea36-154">toomove an integration account tooanother Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ea36-155">Dopo aver spostato un account di integrazione, è necessario aggiornare tutti gli script toouse hello nuovi ID di risorsa.</span><span class="sxs-lookup"><span data-stu-id="2ea36-155">You must update all scripts toouse hello new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="2ea36-156">Selezionare **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-156">Select **More services**.</span></span>

    ![Selezionare "Altri servizi"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="2ea36-158">Nella casella di ricerca hello, digitare "integrazione" per il filtro.</span><span class="sxs-lookup"><span data-stu-id="2ea36-158">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="2ea36-159">Selezionare dall'elenco risultati hello **account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-159">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtro su "integrazione", selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="2ea36-161">Selezionare l'account di integrazione hello che si desidera toomove.</span><span class="sxs-lookup"><span data-stu-id="2ea36-161">Select hello integration account that you want toomove.</span></span> <span data-ttu-id="2ea36-162">In **Impostazioni**, scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="2ea36-162">Under **Settings**, choose **Properties**.</span></span>

    ![Selezionare toomove account di integrazione.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="2ea36-165">Modificare il gruppo di risorse hello o sottoscrizione di Azure che è associato all'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="2ea36-165">Change hello resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Scegliere Cambia il gruppo di risorse o Cambia sottoscrizione](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="2ea36-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2ea36-167">Next Steps</span></span>
* [<span data-ttu-id="2ea36-168">Altre informazioni sui contratti</span><span class="sxs-lookup"><span data-stu-id="2ea36-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  

