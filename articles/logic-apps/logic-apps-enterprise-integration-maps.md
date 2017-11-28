---
title: Trasformare i dati XML con le mappe XSLT - App per la logica di Azure | Microsoft Docs
description: Aggiungere mappe XSLT per trasformare i dati XML con App per la logica di Azure ed Enterprise Integration Pack
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 4445a84a6c6425110e7d705019a28b5cc5447046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="991b5-103">Aggiungere mappe per la trasformazione dei dati XML</span><span class="sxs-lookup"><span data-stu-id="991b5-103">Add maps for XML data transform</span></span>

<span data-ttu-id="991b5-104">Enterprise Integration usa mappe per trasformare i dati XML da un formato all'altro.</span><span class="sxs-lookup"><span data-stu-id="991b5-104">Enterprise integration uses maps to transform XML data between formats.</span></span> <span data-ttu-id="991b5-105">Una mappa è un documento XML che definisce i dati di un documento che devono essere trasformati in un altro formato.</span><span class="sxs-lookup"><span data-stu-id="991b5-105">A map is an XML document that defines the data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="991b5-106">Perché usare le mappe?</span><span class="sxs-lookup"><span data-stu-id="991b5-106">Why use maps?</span></span>

<span data-ttu-id="991b5-107">Si supponga di ricevere regolarmente fatture o ordini B2B da un cliente che usa il formato AAAMMGG per le date.</span><span class="sxs-lookup"><span data-stu-id="991b5-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses the YYYMMDD format for dates.</span></span> <span data-ttu-id="991b5-108">In azienda però le date vengono archiviare nel formato MMGGAAA.</span><span class="sxs-lookup"><span data-stu-id="991b5-108">However, in your organization, you store dates in the MMDDYYY format.</span></span> <span data-ttu-id="991b5-109">È possibile usare una mappa per *trasformare* il formato di data AAAMMGG in MMGGAAA prima di archiviare i dettagli dell'ordine o della fattura nel database relativo.</span><span class="sxs-lookup"><span data-stu-id="991b5-109">You can use a map to *transform* the YYYMMDD date format into the MMDDYYY before storing the order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="991b5-110">Come si crea una mappa?</span><span class="sxs-lookup"><span data-stu-id="991b5-110">How do I create a map?</span></span>

<span data-ttu-id="991b5-111">È possibile creare progetti BizTalk Integration con [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Informazioni su Enterprise Integration Pack") per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="991b5-111">You can create BizTalk Integration projects with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="991b5-112">È quindi possibile creare un file Integration Map che consente di eseguire il mapping visivo degli elementi tra due file di schema XML.</span><span class="sxs-lookup"><span data-stu-id="991b5-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="991b5-113">Dopo aver compilato il progetto, si disporrà di un documento XSLT.</span><span class="sxs-lookup"><span data-stu-id="991b5-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="991b5-114">Come si aggiunge una mappa?</span><span class="sxs-lookup"><span data-stu-id="991b5-114">How do I add a map?</span></span>

1. <span data-ttu-id="991b5-115">Nel Portale di Azure selezionare **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="991b5-115">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="991b5-116">Nella casella di ricerca per filtrare immettere **integrazione**, quindi selezionare **Account di integrazione** dall'elenco dei risultati.</span><span class="sxs-lookup"><span data-stu-id="991b5-116">In the filter search box, enter **integration**, then select **Integration Accounts** from the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="991b5-117">Selezionare l'account di integrazione in cui si desidera aggiungere la mappa.</span><span class="sxs-lookup"><span data-stu-id="991b5-117">Select the integration account where you want to add the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="991b5-118">Selezionare il riquadro **Mappe**.</span><span class="sxs-lookup"><span data-stu-id="991b5-118">Select the **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="991b5-119">Quando il pannello Mappe è aperto, scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="991b5-119">After the Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="991b5-120">Immettere un **nome** per la mappa.</span><span class="sxs-lookup"><span data-stu-id="991b5-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="991b5-121">Per caricare il file di mappa, scegliere l'icona a forma di cartella a destra della casella di testo **Mappa**.</span><span class="sxs-lookup"><span data-stu-id="991b5-121">To upload the map file, choose the folder icon on the right side of the **Map** text box.</span></span> <span data-ttu-id="991b5-122">Al termine del processo di caricamento, scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="991b5-122">After the upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="991b5-123">Dopo che Azure aggiunge la mappa all'account di integrazione, viene visualizzato un messaggio che indica se il file di mappa è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="991b5-123">After Azure adds the map to your integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="991b5-124">Dopo aver visualizzato il messaggio, scegliere il riquadro **Mappe** in modo da visualizzare la mappa appena aggiunta.</span><span class="sxs-lookup"><span data-stu-id="991b5-124">After you get this message, choose the **Maps** tile so you can view the newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="991b5-125">Come si modifica una mappa?</span><span class="sxs-lookup"><span data-stu-id="991b5-125">How do I edit a map?</span></span>

<span data-ttu-id="991b5-126">È necessario caricare un nuovo file di mappa con le modifiche desiderate.</span><span class="sxs-lookup"><span data-stu-id="991b5-126">You must upload a new map file with the changes that you want.</span></span> <span data-ttu-id="991b5-127">È anche possibile scaricare la mappa e poi modificarla.</span><span class="sxs-lookup"><span data-stu-id="991b5-127">You can first download the map for editing.</span></span>

<span data-ttu-id="991b5-128">Per caricare una nuova mappa che sostituisce una mappa esistente, attenersi ai passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="991b5-128">To upload a new map that replaces the existing map, follow these steps.</span></span>

1. <span data-ttu-id="991b5-129">Scegliere il riquadro **Mappe**.</span><span class="sxs-lookup"><span data-stu-id="991b5-129">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="991b5-130">Quando il pannello Mappe è aperto, selezionare la mappa da modificare.</span><span class="sxs-lookup"><span data-stu-id="991b5-130">After the Maps blade opens, select the map that you want to edit.</span></span>

3. <span data-ttu-id="991b5-131">Nel pannello **Mappe** scegliere **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="991b5-131">On the **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="991b5-132">Nella selezione file selezionare il file di mappa da caricare, quindi scegliere **Apri**.</span><span class="sxs-lookup"><span data-stu-id="991b5-132">In the file picker, select the map file that you want to upload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-to-delete-a-map"></a><span data-ttu-id="991b5-133">Come eliminare una mappa?</span><span class="sxs-lookup"><span data-stu-id="991b5-133">How to delete a map?</span></span>

1. <span data-ttu-id="991b5-134">Scegliere il riquadro **Mappe**.</span><span class="sxs-lookup"><span data-stu-id="991b5-134">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="991b5-135">Quando il pannello Mappe è aperto, selezionare la mappa da eliminare.</span><span class="sxs-lookup"><span data-stu-id="991b5-135">After the Maps blade opens, select the map you want to delete.</span></span>

3. <span data-ttu-id="991b5-136">Scegliere **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="991b5-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="991b5-137">Confermare che si desidera eliminare la mappa.</span><span class="sxs-lookup"><span data-stu-id="991b5-137">Confirm that you want to delete the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="991b5-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="991b5-138">Next Steps</span></span>
* [<span data-ttu-id="991b5-139">Altre informazioni su Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="991b5-139">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Informazioni su Enterprise Integration Pack")  
* [<span data-ttu-id="991b5-140">Altre informazioni sui contratti</span><span class="sxs-lookup"><span data-stu-id="991b5-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  
* [<span data-ttu-id="991b5-141">Altre informazioni sulle trasformazioni</span><span class="sxs-lookup"><span data-stu-id="991b5-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Informazioni sulle trasformazioni di Enterprise Integration")  

