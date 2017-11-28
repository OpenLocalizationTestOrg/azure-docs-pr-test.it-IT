---
title: Creare, collegare, eliminare o spostare un account di integrazione in App per la logica di Azure | Documentazione Microsoft
description: Come creare un account di integrazione e collegarlo ad app per la logica
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
ms.openlocfilehash: 716e7b5bab8725dea0fd2b760d0e46e8e892c5b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="1d191-103">Cos'è un account di integrazione?</span><span class="sxs-lookup"><span data-stu-id="1d191-103">What is an integration account?</span></span>

<span data-ttu-id="1d191-104">Un account di integrazione consente alle app di integrazione aziendale di gestire elementi diversi, ad esempio schemi, mappe, certificati, partner e contratti.</span><span class="sxs-lookup"><span data-stu-id="1d191-104">An integration account allows enterprise integration apps to manage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="1d191-105">Qualsiasi applicazione di integrazione create usa un account di integrazione per accedere a tali schemi, mappe, certificati e così via.</span><span class="sxs-lookup"><span data-stu-id="1d191-105">Any integration app you create uses an integration account to access these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="1d191-106">Creare un account di integrazione</span><span class="sxs-lookup"><span data-stu-id="1d191-106">Create an integration account</span></span>

1.  <span data-ttu-id="1d191-107">Accedere al [Portale di Azure](http://portal.azure.com "Portale di Azure").</span><span class="sxs-lookup"><span data-stu-id="1d191-107">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="1d191-108">Fare clic su **Altri servizi** nel menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="1d191-108">From the left menu, select **More services**.</span></span>

    ![Selezionare "Altri servizi"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="1d191-110">Nella casella di ricerca, digitare "integrazione" come filtro.</span><span class="sxs-lookup"><span data-stu-id="1d191-110">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="1d191-111">Nell'elenco dei risultati selezionare **Account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="1d191-111">In the results list, select **Integration Accounts**.</span></span>

    ![Filtro su "integrazione", selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="1d191-113">Nella parte superiore della pagina fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="1d191-113">At the top of the page, choose **Add**.</span></span>

    ![Scegliere Aggiungi](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="1d191-115">Denominare l'account di integrazione e selezionare la sottoscrizione di Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="1d191-115">Name your integration account and select the Azure subscription that you want to use.</span></span> <span data-ttu-id="1d191-116">È possibile creare un nuovo **Gruppo di risorse** o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="1d191-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="1d191-117">Selezionare quindi la **località** in cui eseguire l'hosting dell'account di integrazione e un **piano tariffario**.</span><span class="sxs-lookup"><span data-stu-id="1d191-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="1d191-118">Al termine, scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="1d191-118">When you're ready, choose **Create**.</span></span>

    ![Immettere i dettagli dell'account di integrazione](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="1d191-120">Azure esegue il provisioning dell'account di integrazione nella località selezionata. L'esecuzione dell'operazione dura circa 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="1d191-120">Azure provisions your integration account  in the selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="1d191-121">Aggiornare la pagina.</span><span class="sxs-lookup"><span data-stu-id="1d191-121">Refresh the page.</span></span> <span data-ttu-id="1d191-122">Il nuovo account di integrazione verrà visualizzato nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="1d191-122">You see your new integration account listed.</span></span>

    ![Visualizzazione del nuovo account di integrazione](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="1d191-124">Collegare quindi l'account di integrazione creato all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="1d191-124">Next, link the integration account that you created to your logic app.</span></span> 

## <a name="link-an-integration-account-to-a-logic-app"></a><span data-ttu-id="1d191-125">Collegare un account di integrazione a un'app per la logica</span><span class="sxs-lookup"><span data-stu-id="1d191-125">Link an integration account to a logic app</span></span>

<span data-ttu-id="1d191-126">Per consentire alle app per la logica di accedere a mappe, schemi, contratti e altri elementi nell'account di integrazione, collegare quest'ultimo all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="1d191-126">To give your logic apps access to maps, schemas, agreements, and other artifacts in your integration account, link the integration account to your logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1d191-127">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1d191-127">Prerequisites</span></span>

* <span data-ttu-id="1d191-128">Un account di integrazione</span><span class="sxs-lookup"><span data-stu-id="1d191-128">An integration account</span></span>
* <span data-ttu-id="1d191-129">App per la logica</span><span class="sxs-lookup"><span data-stu-id="1d191-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="1d191-130">Prima di iniziare, assicurarsi che l'account di integrazione e l'app per la logica si trovino nella *stessa posizione di Azure*.</span><span class="sxs-lookup"><span data-stu-id="1d191-130">Make sure your integration account and logic app are in the *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="1d191-131">Nel portale di Azure, selezionare l'app per la logica e controllarne la località.</span><span class="sxs-lookup"><span data-stu-id="1d191-131">In the Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Selezionare l'app per la logica, controllare la località](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="1d191-133">In **Impostazioni**, selezionare **Account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="1d191-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="1d191-135">Nell'elenco**Selezionare un account di integrazione** selezionare l'account di integrazione da collegare all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="1d191-135">From the **Select an Integration account** list, select the integration account you want to link to your logic app.</span></span> <span data-ttu-id="1d191-136">Per completare il collegamento, selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="1d191-136">To finish linking, choose **Save**.</span></span>

    ![Selezionare l'account di integrazione](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="1d191-138">Viene visualizzata una notifica con l'avviso che l'account di integrazione è stato collegato all'app per la logica e che tutti gli elementi nell'account di integrazione sono ora disponibili.</span><span class="sxs-lookup"><span data-stu-id="1d191-138">You get a notification that shows your integration account is linked to your logic app,  and that all artifacts in your integration account are now available to your logic app.</span></span>

    ![L'app per la logica è collegata all'account di integrazione.](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="1d191-140">Ora che l'account di integrazione è collegato all'app per la logica, è possibile usare i connettori B2B presenti nelle app per la logica.</span><span class="sxs-lookup"><span data-stu-id="1d191-140">Now that your integration account is linked to your logic app, you can use the B2B connectors in your logic apps.</span></span> <span data-ttu-id="1d191-141">Alcuni connettori B2B comuni includono la convalida XML e la codifica e decodifica di file flat.</span><span class="sxs-lookup"><span data-stu-id="1d191-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="1d191-142">Eliminare l'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="1d191-142">Delete your integration account</span></span>

1. <span data-ttu-id="1d191-143">Selezionare **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="1d191-143">Select **More services**.</span></span>

    ![Selezionare "Altri servizi"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="1d191-145">Nella casella di ricerca, digitare "integrazione" come filtro.</span><span class="sxs-lookup"><span data-stu-id="1d191-145">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="1d191-146">Nell'elenco dei risultati selezionare **Account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="1d191-146">In the results list, select **Integration Accounts**.</span></span>

    ![Filtro su "integrazione", selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="1d191-148">Selezionare l'account di integrazione da eliminare.</span><span class="sxs-lookup"><span data-stu-id="1d191-148">Select the integration account that you want to delete.</span></span>

    ![Selezionare l'account di integrazione da eliminare](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="1d191-150">Dal menu, scegliere **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="1d191-150">On the menu, choose **Delete**.</span></span>

    ![Scegliere "Elimina"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="1d191-152">Confermare la scelta di eliminazione dell'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="1d191-152">Confirm your choice to delete the integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="1d191-153">Spostare l'account di integrazione</span><span class="sxs-lookup"><span data-stu-id="1d191-153">Move your integration account</span></span>

<span data-ttu-id="1d191-154">Per spostare un account di integrazione a un'altra sottoscrizione o gruppo di risorse di Azure, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="1d191-154">To move an integration account to another Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d191-155">Dopo lo spostamento di un account di integrazione è necessario aggiornare tutti gli script in modo che usino i nuovi ID risorsa.</span><span class="sxs-lookup"><span data-stu-id="1d191-155">You must update all scripts to use the new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="1d191-156">Selezionare **Altri servizi**.</span><span class="sxs-lookup"><span data-stu-id="1d191-156">Select **More services**.</span></span>

    ![Selezionare "Altri servizi"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="1d191-158">Nella casella di ricerca, digitare "integrazione" come filtro.</span><span class="sxs-lookup"><span data-stu-id="1d191-158">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="1d191-159">Nell'elenco dei risultati selezionare **Account di integrazione**.</span><span class="sxs-lookup"><span data-stu-id="1d191-159">In the results list, select **Integration Accounts**.</span></span>

    ![Filtro su "integrazione", selezionare "Account di integrazione"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="1d191-161">Selezionare l'account di integrazione da spostare.</span><span class="sxs-lookup"><span data-stu-id="1d191-161">Select the integration account that you want to move.</span></span> <span data-ttu-id="1d191-162">In **Impostazioni**, scegliere **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="1d191-162">Under **Settings**, choose **Properties**.</span></span>

    ![Selezionare l'account di integrazione da spostare.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="1d191-165">Modificare il gruppo di risorse o la sottoscrizione di Azure associati all'account di integrazione.</span><span class="sxs-lookup"><span data-stu-id="1d191-165">Change the resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Scegliere Cambia il gruppo di risorse o Cambia sottoscrizione](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="1d191-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d191-167">Next Steps</span></span>
* [<span data-ttu-id="1d191-168">Altre informazioni sui contratti</span><span class="sxs-lookup"><span data-stu-id="1d191-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  

