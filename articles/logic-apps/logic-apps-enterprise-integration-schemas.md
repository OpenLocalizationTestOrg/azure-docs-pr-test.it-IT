---
title: aaaSchemas per la convalida XML - App Azure per la logica | Documenti Microsoft
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
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a><span data-ttu-id="4b427-103">Convalida XML con schemi per le app di logica di Azure e hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="4b427-103">Validate XML with schemas for Azure Logic Apps and hello Enterprise Integration Pack</span></span>

<span data-ttu-id="4b427-104">Schemi confermare che si riceve i documenti XML hello siano validi e sia hello previsto i dati in un formato predefinito.</span><span class="sxs-lookup"><span data-stu-id="4b427-104">Schemas confirm that hello XML documents you receive are valid and have hello expected data in a predefined format.</span></span> <span data-ttu-id="4b427-105">Gli schemi vengono usati inoltre per convalidare i messaggi scambiati in uno scenario B2B.</span><span class="sxs-lookup"><span data-stu-id="4b427-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="4b427-106">Aggiungere uno schema</span><span class="sxs-lookup"><span data-stu-id="4b427-106">Add a schema</span></span>

1. <span data-ttu-id="4b427-107">Nel portale di Azure hello, selezionare **più servizi**.</span><span class="sxs-lookup"><span data-stu-id="4b427-107">In hello Azure portal, select **More services**.</span></span>

    ![Portale di Azure, "More services" (Altri servizi)](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="4b427-109">Nella casella di ricerca hello filtro immettere **integrazione**e selezionare **account di integrazione** dall'elenco dei risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="4b427-109">In hello filter search box, enter **integration**, and select **Integration Accounts** from hello results list.</span></span>

    ![Casella di ricerca del filtro](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="4b427-111">Seleziona hello **account integrazione** in cui si desidera schema hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4b427-111">Select hello **integration account** where you want tooadd hello schema.</span></span>

    ![Elenco degli account di integrazione](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="4b427-113">Scegliere hello **schemi** riquadro.</span><span class="sxs-lookup"><span data-stu-id="4b427-113">Choose hello **Schemas** tile.</span></span>

    ![Esempio di account di integrazione, "Schemi"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="4b427-115">Aggiungere un file di schema di dimensioni inferiori a 2 MB</span><span class="sxs-lookup"><span data-stu-id="4b427-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="4b427-116">In hello **schemi** blade che viene visualizzata (da hello passaggi precedenti), scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4b427-116">In hello **Schemas** blade that opens (from hello preceding steps), choose **Add**.</span></span>

    ![Pannello Schemi, "Aggiungi"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="4b427-118">Immettere un nome per lo schema.</span><span class="sxs-lookup"><span data-stu-id="4b427-118">Enter a name for your schema.</span></span> <span data-ttu-id="4b427-119">Caricare il file di schema hello selezionando hello cartella icona Avanti toohello **Schema** casella.</span><span class="sxs-lookup"><span data-stu-id="4b427-119">Upload hello schema file by selecting hello folder icon next toohello **Schema** box.</span></span> <span data-ttu-id="4b427-120">Al termine del processo di caricamento hello, **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b427-120">After hello upload process completes, select **OK**.</span></span>

    ![Screenshot di "Aggiungi schema", con "File piccolo" evidenziato](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a><span data-ttu-id="4b427-122">Aggiungere un file di schema maggiore di 2 MB (backup di un massimo di too8 MB)</span><span class="sxs-lookup"><span data-stu-id="4b427-122">Add a schema file larger than 2 MB (up too8 MB maximum)</span></span>

<span data-ttu-id="4b427-123">Questi passaggi sono diversi in base ai livelli di accesso di contenitore blob hello: **pubblica** o **Nessun accesso anonimo**.</span><span class="sxs-lookup"><span data-stu-id="4b427-123">These steps differ based on hello blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="4b427-124">**toodetermine questo livello di accesso**</span><span class="sxs-lookup"><span data-stu-id="4b427-124">**toodetermine this access level**</span></span>

1.  <span data-ttu-id="4b427-125">Aprire **Azure Storage Explorer** (Esplora archivi di Azure).</span><span class="sxs-lookup"><span data-stu-id="4b427-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="4b427-126">In **contenitori Blob**, selezionare il contenitore di blob hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="4b427-126">Under **Blob Containers**, select hello blob container you want.</span></span> 

3.  <span data-ttu-id="4b427-127">Selezionare **Sicurezza**, **Livello di accesso**.</span><span class="sxs-lookup"><span data-stu-id="4b427-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="4b427-128">Se è a livello di accesso di sicurezza blob hello **pubblica**, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="4b427-128">If hello blob security access level is **Public**, follow these steps.</span></span>

![Azure Storage Explorer con evidenziate le opzioni "Contenitori BLOB", "Sicurezza" e "Pubblico"](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="4b427-130">Caricare l'account di archiviazione tooyour schema hello e copiare hello URI.</span><span class="sxs-lookup"><span data-stu-id="4b427-130">Upload hello schema tooyour storage account, and copy hello URI.</span></span>

    ![Account di archiviazione con URI evidenziato](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="4b427-132">In **Aggiungi Schema**selezionare **file di grandi dimensioni**e fornire Ciao URI hello **URI contenuto** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="4b427-132">In **Add Schema**, select **Large file**, and provide hello URI in hello **Content URI** text box.</span></span>

    ![Schemi con evidenziati il pulsante "Aggiungi" e l'opzione "Large file" (File grande)](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="4b427-134">Se è a livello di accesso di sicurezza blob hello **Nessun accesso anonimo**, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="4b427-134">If hello blob security access level is **No anonymous access**, follow these steps.</span></span>

![Azure Storage Explorer, con evidenziate le opzioni "Contenitori BLOB", "Sicurezza" e "No anonymous access" (Nessun accesso anonimo)](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="4b427-136">Caricare l'account di archiviazione tooyour hello dello schema.</span><span class="sxs-lookup"><span data-stu-id="4b427-136">Upload hello schema tooyour storage account.</span></span>

    ![Account di archiviazione](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="4b427-138">Generare una firma di accesso condiviso per lo schema di hello.</span><span class="sxs-lookup"><span data-stu-id="4b427-138">Generate a shared access signature for hello schema.</span></span>

    ![Account di archiviazione con evidenziata la scheda delle firme di accesso condiviso](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="4b427-140">In **Aggiungi Schema**selezionare **file di grandi dimensioni**e fornire una firma di accesso condiviso hello URI in hello **URI contenuto** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="4b427-140">In **Add Schema**, select **Large file**, and provide hello shared access signature URI in hello **Content URI** text box.</span></span>

    ![Schemi con evidenziati il pulsante "Aggiungi" e l'opzione "Large file" (File grande)](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="4b427-142">In hello **schemi** pannello dell'account di integrazione, dovrebbe essere visualizzato il nuovo schema.</span><span class="sxs-lookup"><span data-stu-id="4b427-142">In hello **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![L'account di integrazione, con "Schemi" e il nuovo schema hello evidenziato](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="4b427-144">Modificare gli schemi</span><span class="sxs-lookup"><span data-stu-id="4b427-144">Edit schemas</span></span>

1. <span data-ttu-id="4b427-145">Scegliere hello **schemi** riquadro.</span><span class="sxs-lookup"><span data-stu-id="4b427-145">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="4b427-146">Dopo aver hello **schemi** pannello consente di aprire, schema selezionare hello che si desidera tooedit.</span><span class="sxs-lookup"><span data-stu-id="4b427-146">After hello **Schemas** blade opens, select hello schema that you want tooedit.</span></span>

3. <span data-ttu-id="4b427-147">In hello **schemi** pannello, scegliere **modifica**.</span><span class="sxs-lookup"><span data-stu-id="4b427-147">On hello **Schemas** blade, choose **Edit**.</span></span>

    ![Pannello Schemi](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="4b427-149">File di schema selezionare hello che si desidera tooedit, quindi selezionare **aprire**.</span><span class="sxs-lookup"><span data-stu-id="4b427-149">Select hello schema file that you want tooedit, then select **Open**.</span></span>

    ![Apri schema file tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="4b427-151">Azure Visualizza un messaggio che hello schema caricato correttamente.</span><span class="sxs-lookup"><span data-stu-id="4b427-151">Azure shows a message that hello schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="4b427-152">Eliminare gli schemi</span><span class="sxs-lookup"><span data-stu-id="4b427-152">Delete schemas</span></span>

1. <span data-ttu-id="4b427-153">Scegliere hello **schemi** riquadro.</span><span class="sxs-lookup"><span data-stu-id="4b427-153">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="4b427-154">Dopo aver hello **schemi** pannello consente di aprire, schema selezionare hello desiderato toodelete.</span><span class="sxs-lookup"><span data-stu-id="4b427-154">After hello **Schemas** blade opens, select hello schema you want toodelete.</span></span>

3. <span data-ttu-id="4b427-155">In hello **schemi** pannello, scegliere **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="4b427-155">On hello **Schemas** blade, choose **Delete**.</span></span>

    ![Pannello Schemi](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="4b427-157">tooconfirm che si desidera toodelete hello selezionata dello schema, scegliere **Sì**.</span><span class="sxs-lookup"><span data-stu-id="4b427-157">tooconfirm that you want toodelete hello selected schema, choose **Yes**.</span></span>

    ![Messaggio di conferma "Elimina schema"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="4b427-159">In hello **schemi** pannello elenco schema hello viene aggiornata e non include più schema hello che è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="4b427-159">In hello **Schemas** blade, hello schema list refreshes  and no longer includes hello schema that you deleted.</span></span>

    ![Account di integrazione con il riquadro "Schemi" evidenziato](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="4b427-161">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b427-161">Next steps</span></span>
* <span data-ttu-id="4b427-162">[Altre informazioni su Enterprise Integration Pack hello](logic-apps-enterprise-integration-overview.md "informazioni sul pacchetto di integrazione di enterprise hello").</span><span class="sxs-lookup"><span data-stu-id="4b427-162">[Learn more about hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack").</span></span>  

