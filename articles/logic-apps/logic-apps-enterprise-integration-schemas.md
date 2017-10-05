---
title: Schemi per la convalida XML - App per la logica di Azure | Microsoft Docs
description: Convalida dei documenti XML con gli schemi per le app per la logica di Azure ed Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 4f58a587c1f10aea1cee89e46fa9ec340e0d21c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-the-enterprise-integration-pack"></a><span data-ttu-id="57cca-103">Convalida XML con gli schemi per le app per la logica di Azure ed Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="57cca-103">Validate XML with schemas for Azure Logic Apps and the Enterprise Integration Pack</span></span>

<span data-ttu-id="57cca-104">È possibile usare gli schemi per confermare che i documenti XML ricevuti siano validi e avere i dati previsti in un formato predefinito.</span><span class="sxs-lookup"><span data-stu-id="57cca-104">Schemas confirm that the XML documents you receive are valid and have the expected data in a predefined format.</span></span> <span data-ttu-id="57cca-105">Gli schemi vengono usati inoltre per convalidare i messaggi scambiati in uno scenario B2B.</span><span class="sxs-lookup"><span data-stu-id="57cca-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="57cca-106">Aggiungere uno schema</span><span class="sxs-lookup"><span data-stu-id="57cca-106">Add a schema</span></span>

1. <span data-ttu-id="57cca-107">Nel Portale di Azure fare clic su **More services** (Altri servizi).</span><span class="sxs-lookup"><span data-stu-id="57cca-107">In the Azure portal, select **More services**.</span></span>

    ![Portale di Azure, "More services" (Altri servizi)](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="57cca-109">Nella casella di ricerca del filtro immettere **integrazione**, quindi selezionare **Account di integrazione** dall'elenco dei risultati.</span><span class="sxs-lookup"><span data-stu-id="57cca-109">In the filter search box, enter **integration**, and select **Integration Accounts** from the results list.</span></span>

    ![Casella di ricerca del filtro](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="57cca-111">Selezionare l'**account di integrazione** in cui si desidera aggiungere lo schema.</span><span class="sxs-lookup"><span data-stu-id="57cca-111">Select the **integration account** where you want to add the schema.</span></span>

    ![Elenco degli account di integrazione](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="57cca-113">Selezionare il riquadro **Schemi**.</span><span class="sxs-lookup"><span data-stu-id="57cca-113">Choose the **Schemas** tile.</span></span>

    ![Esempio di account di integrazione, "Schemi"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="57cca-115">Aggiungere un file di schema di dimensioni inferiori a 2 MB</span><span class="sxs-lookup"><span data-stu-id="57cca-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="57cca-116">Nel pannello **Schemi** visualizzato nei passaggi precedenti, selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="57cca-116">In the **Schemas** blade that opens (from the preceding steps), choose **Add**.</span></span>

    ![Pannello Schemi, "Aggiungi"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="57cca-118">Immettere un nome per lo schema.</span><span class="sxs-lookup"><span data-stu-id="57cca-118">Enter a name for your schema.</span></span> <span data-ttu-id="57cca-119">Caricare il file di schema selezionando l'icona della cartella accanto alla casella di testo **Schema**.</span><span class="sxs-lookup"><span data-stu-id="57cca-119">Upload the schema file by selecting the folder icon next to the **Schema** box.</span></span> <span data-ttu-id="57cca-120">Al termine del processo di caricamento, scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="57cca-120">After the upload process completes, select **OK**.</span></span>

    ![Screenshot di "Aggiungi schema", con "File piccolo" evidenziato](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-to-8-mb-maximum"></a><span data-ttu-id="57cca-122">Aggiungere un file di schema di dimensioni maggiori di 2 MB (fino a un massimo di 8 MB)</span><span class="sxs-lookup"><span data-stu-id="57cca-122">Add a schema file larger than 2 MB (up to 8 MB maximum)</span></span>

<span data-ttu-id="57cca-123">La procedura dipende dal livello di accesso del contenitore BLOB, ovvero **Pubblico** o **Nessun accesso anonimo**.</span><span class="sxs-lookup"><span data-stu-id="57cca-123">These steps differ based on the blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="57cca-124">**Per determinare il livello di accesso**</span><span class="sxs-lookup"><span data-stu-id="57cca-124">**To determine this access level**</span></span>

1.  <span data-ttu-id="57cca-125">Aprire **Azure Storage Explorer** (Esplora archivi di Azure).</span><span class="sxs-lookup"><span data-stu-id="57cca-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="57cca-126">In **Contenitori Blob**, selezionare il contenitore di blob desiderato.</span><span class="sxs-lookup"><span data-stu-id="57cca-126">Under **Blob Containers**, select the blob container you want.</span></span> 

3.  <span data-ttu-id="57cca-127">Selezionare **Sicurezza**, **Livello di accesso**.</span><span class="sxs-lookup"><span data-stu-id="57cca-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="57cca-128">Se il livello di accesso di sicurezza del BLOB è **Pubblico**, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="57cca-128">If the blob security access level is **Public**, follow these steps.</span></span>

![Azure Storage Explorer con evidenziate le opzioni "Contenitori BLOB", "Sicurezza" e "Pubblico"](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="57cca-130">Caricare lo schema nell'account di archiviazione e copiare l'URI.</span><span class="sxs-lookup"><span data-stu-id="57cca-130">Upload the schema to your storage account, and copy the URI.</span></span>

    ![Account di archiviazione con URI evidenziato](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="57cca-132">In **Aggiungi schema** selezionare **File grande**, quindi specificare l'URI nella casella di testo **URI del contenuto**.</span><span class="sxs-lookup"><span data-stu-id="57cca-132">In **Add Schema**, select **Large file**, and provide the URI in the **Content URI** text box.</span></span>

    ![Schemi con evidenziati il pulsante "Aggiungi" e l'opzione "Large file" (File grande)](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="57cca-134">Se il livello di accesso di sicurezza BLOB è **Nessun accesso anonimo**, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="57cca-134">If the blob security access level is **No anonymous access**, follow these steps.</span></span>

![Azure Storage Explorer, con evidenziate le opzioni "Contenitori BLOB", "Sicurezza" e "No anonymous access" (Nessun accesso anonimo)](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="57cca-136">Caricare lo schema nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="57cca-136">Upload the schema to your storage account.</span></span>

    ![Account di archiviazione](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="57cca-138">Generare una firma di accesso condiviso per lo schema.</span><span class="sxs-lookup"><span data-stu-id="57cca-138">Generate a shared access signature for the schema.</span></span>

    ![Account di archiviazione con evidenziata la scheda delle firme di accesso condiviso](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="57cca-140">In **Aggiungi schema**, selezionare **File grande**, quindi specificare l'URI della firma di accesso condiviso nella casella di testo **URI del contenuto**.</span><span class="sxs-lookup"><span data-stu-id="57cca-140">In **Add Schema**, select **Large file**, and provide the shared access signature URI in the **Content URI** text box.</span></span>

    ![Schemi con evidenziati il pulsante "Aggiungi" e l'opzione "Large file" (File grande)](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="57cca-142">Nel pannello **Schemi** dell'account di integrazione dovrebbe essere visualizzato lo schema appena aggiunto.</span><span class="sxs-lookup"><span data-stu-id="57cca-142">In the **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![Account di integrazione EIP con evidenziati il pannello "Schemi" e il nuovo schema](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="57cca-144">Modificare gli schemi</span><span class="sxs-lookup"><span data-stu-id="57cca-144">Edit schemas</span></span>

1. <span data-ttu-id="57cca-145">Selezionare il riquadro **Schemi**.</span><span class="sxs-lookup"><span data-stu-id="57cca-145">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="57cca-146">Selezionare lo schema da modificare quando il pannello **Schemi** si apre.</span><span class="sxs-lookup"><span data-stu-id="57cca-146">After the **Schemas** blade opens, select the schema that you want to edit.</span></span>

3. <span data-ttu-id="57cca-147">Nel pannello **Schemi** selezionare **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="57cca-147">On the **Schemas** blade, choose **Edit**.</span></span>

    ![Pannello Schemi](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="57cca-149">Selezionare il file di schema che si desidera modificare, quindi selezionare **Apri**.</span><span class="sxs-lookup"><span data-stu-id="57cca-149">Select the schema file that you want to edit, then select **Open**.</span></span>

    ![Aprire il file di schema da modificare](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="57cca-151">In Azure viene visualizzato il messaggio che lo schema è stato caricato correttamente.</span><span class="sxs-lookup"><span data-stu-id="57cca-151">Azure shows a message that the schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="57cca-152">Eliminare gli schemi</span><span class="sxs-lookup"><span data-stu-id="57cca-152">Delete schemas</span></span>

1. <span data-ttu-id="57cca-153">Selezionare il riquadro **Schemi**.</span><span class="sxs-lookup"><span data-stu-id="57cca-153">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="57cca-154">Selezionare lo schema da eliminare quando il pannello **Schemi** si apre.</span><span class="sxs-lookup"><span data-stu-id="57cca-154">After the **Schemas** blade opens, select the schema you want to delete.</span></span>

3. <span data-ttu-id="57cca-155">Nel pannello **Schemi** selezionare **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="57cca-155">On the **Schemas** blade, choose **Delete**.</span></span>

    ![Pannello Schemi](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="57cca-157">Per confermare che si desidera eliminare lo schema selezionato scegliere **Sì**.</span><span class="sxs-lookup"><span data-stu-id="57cca-157">To confirm that you want to delete the selected schema, choose **Yes**.</span></span>

    ![Messaggio di conferma "Elimina schema"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="57cca-159">Nel pannello **Schemi** si aggiorna l'elenco degli schemi, che non include più lo schema che è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="57cca-159">In the **Schemas** blade, the schema list refreshes  and no longer includes the schema that you deleted.</span></span>

    ![Account di integrazione con il riquadro "Schemi" evidenziato](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="57cca-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="57cca-161">Next steps</span></span>
* <span data-ttu-id="57cca-162">[Altre informazioni su Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Informazioni su Enterprise Integration Pack").</span><span class="sxs-lookup"><span data-stu-id="57cca-162">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack").</span></span>  

