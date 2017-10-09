---
title: aaaTransform XML con XSLT mappe - App Azure per la logica | Documenti Microsoft
description: Aggiungere che XSLT esegue il mapping di dati XML tootransform con le applicazioni di logica di Azure e hello Enterprise Integration Pack
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
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="c3a57-103">Aggiungere mappe per la trasformazione dei dati XML</span><span class="sxs-lookup"><span data-stu-id="c3a57-103">Add maps for XML data transform</span></span>

<span data-ttu-id="c3a57-104">Utilizza integrazione di Enterprise esegue il mapping dei dati XML tootransform tra formati.</span><span class="sxs-lookup"><span data-stu-id="c3a57-104">Enterprise integration uses maps tootransform XML data between formats.</span></span> <span data-ttu-id="c3a57-105">Una mappa è un documento XML che definisce i dati hello in un documento che deve essere trasformato in un altro formato.</span><span class="sxs-lookup"><span data-stu-id="c3a57-105">A map is an XML document that defines hello data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="c3a57-106">Perché usare le mappe?</span><span class="sxs-lookup"><span data-stu-id="c3a57-106">Why use maps?</span></span>

<span data-ttu-id="c3a57-107">Si supponga che riceve regolarmente B2B ordini o fatture da un cliente che utilizza il formato YYYMMDD hello per le date.</span><span class="sxs-lookup"><span data-stu-id="c3a57-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses hello YYYMMDD format for dates.</span></span> <span data-ttu-id="c3a57-108">All'interno dell'organizzazione, tuttavia, archiviare le date nel formato MMDDYYY hello.</span><span class="sxs-lookup"><span data-stu-id="c3a57-108">However, in your organization, you store dates in hello MMDDYYY format.</span></span> <span data-ttu-id="c3a57-109">È possibile utilizzare una mappa troppo*trasformare* formato di data YYYMMDD hello in hello MMDDYYY prima di archiviare i dettagli dell'ordine o una fattura hello nel database di attività dei clienti.</span><span class="sxs-lookup"><span data-stu-id="c3a57-109">You can use a map too*transform* hello YYYMMDD date format into hello MMDDYYY before storing hello order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="c3a57-110">Come si crea una mappa?</span><span class="sxs-lookup"><span data-stu-id="c3a57-110">How do I create a map?</span></span>

<span data-ttu-id="c3a57-111">È possibile creare progetti di integrazione di BizTalk con hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "informazioni sul pacchetto di integrazione di enterprise hello") per Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="c3a57-111">You can create BizTalk Integration projects with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="c3a57-112">È quindi possibile creare un file Integration Map che consente di eseguire il mapping visivo degli elementi tra due file di schema XML.</span><span class="sxs-lookup"><span data-stu-id="c3a57-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="c3a57-113">Dopo aver compilato il progetto, si disporrà di un documento XSLT.</span><span class="sxs-lookup"><span data-stu-id="c3a57-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="c3a57-114">Come si aggiunge una mappa?</span><span class="sxs-lookup"><span data-stu-id="c3a57-114">How do I add a map?</span></span>

1. <span data-ttu-id="c3a57-115">Nel portale di Azure hello, selezionare **Sfoglia**.</span><span class="sxs-lookup"><span data-stu-id="c3a57-115">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="c3a57-116">Nella casella di ricerca hello filtro immettere **integrazione**, quindi selezionare **account di integrazione** dall'elenco dei risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="c3a57-116">In hello filter search box, enter **integration**, then select **Integration Accounts** from hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="c3a57-117">Selezionare l'account di integrazione hello in cui si desidera mappa hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="c3a57-117">Select hello integration account where you want tooadd hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="c3a57-118">Seleziona hello **mappe** riquadro.</span><span class="sxs-lookup"><span data-stu-id="c3a57-118">Select hello **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="c3a57-119">Dopo l'apertura di blade mappe hello, scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="c3a57-119">After hello Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="c3a57-120">Immettere un **nome** per la mappa.</span><span class="sxs-lookup"><span data-stu-id="c3a57-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="c3a57-121">mappa di hello tooupload file, scegliere l'icona della cartella hello sul lato destro hello di hello **mappa** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="c3a57-121">tooupload hello map file, choose hello folder icon on hello right side of hello **Map** text box.</span></span> <span data-ttu-id="c3a57-122">Al termine del processo di caricamento hello, scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="c3a57-122">After hello upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="c3a57-123">Dopo che Azure aggiunge l'account di integrazione tooyour hello mappa, viene visualizzato un messaggio sullo schermo che mostra se il file di mapping è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="c3a57-123">After Azure adds hello map tooyour integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="c3a57-124">Dopo il messaggio viene visualizzato, scegliere hello **mappe** riquadro in modo da visualizzare hello appena aggiunto mappa.</span><span class="sxs-lookup"><span data-stu-id="c3a57-124">After you get this message, choose hello **Maps** tile so you can view hello newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="c3a57-125">Come si modifica una mappa?</span><span class="sxs-lookup"><span data-stu-id="c3a57-125">How do I edit a map?</span></span>

<span data-ttu-id="c3a57-126">È necessario caricare un nuovo file di mappa con modifiche hello che si desidera.</span><span class="sxs-lookup"><span data-stu-id="c3a57-126">You must upload a new map file with hello changes that you want.</span></span> <span data-ttu-id="c3a57-127">È possibile scaricare innanzitutto mappa hello per la modifica.</span><span class="sxs-lookup"><span data-stu-id="c3a57-127">You can first download hello map for editing.</span></span>

<span data-ttu-id="c3a57-128">tooupload una nuova mappa che sostituisce una mappa esistente hello, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="c3a57-128">tooupload a new map that replaces hello existing map, follow these steps.</span></span>

1. <span data-ttu-id="c3a57-129">Scegliere hello **mappe** riquadro.</span><span class="sxs-lookup"><span data-stu-id="c3a57-129">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="c3a57-130">Dopo l'apertura di blade mappe hello, selezionare la mappa di hello che si desidera tooedit.</span><span class="sxs-lookup"><span data-stu-id="c3a57-130">After hello Maps blade opens, select hello map that you want tooedit.</span></span>

3. <span data-ttu-id="c3a57-131">In hello **mappe** pannello, scegliere **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="c3a57-131">On hello **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="c3a57-132">In selezione file hello, selezionare i file di mappa hello che si desidera tooupload, quindi selezionare **aprire**.</span><span class="sxs-lookup"><span data-stu-id="c3a57-132">In hello file picker, select hello map file that you want tooupload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a><span data-ttu-id="c3a57-133">Come toodelete una mappa?</span><span class="sxs-lookup"><span data-stu-id="c3a57-133">How toodelete a map?</span></span>

1. <span data-ttu-id="c3a57-134">Scegliere hello **mappe** riquadro.</span><span class="sxs-lookup"><span data-stu-id="c3a57-134">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="c3a57-135">Dopo l'apertura di blade mappe hello, selezionare mappa hello che si desidera toodelete.</span><span class="sxs-lookup"><span data-stu-id="c3a57-135">After hello Maps blade opens, select hello map you want toodelete.</span></span>

3. <span data-ttu-id="c3a57-136">Scegliere **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="c3a57-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="c3a57-137">Confermare che si desidera mappa hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="c3a57-137">Confirm that you want toodelete hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="c3a57-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c3a57-138">Next Steps</span></span>
* [<span data-ttu-id="c3a57-139">Altre informazioni su Enterprise Integration Pack hello</span><span class="sxs-lookup"><span data-stu-id="c3a57-139">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "apprendere Enterprise Integration Pack")  
* [<span data-ttu-id="c3a57-140">Altre informazioni sui contratti</span><span class="sxs-lookup"><span data-stu-id="c3a57-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Informazioni sui contratti di Enterprise Integration")  
* [<span data-ttu-id="c3a57-141">Altre informazioni sulle trasformazioni</span><span class="sxs-lookup"><span data-stu-id="c3a57-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Informazioni sulle trasformazioni di Enterprise Integration")  

