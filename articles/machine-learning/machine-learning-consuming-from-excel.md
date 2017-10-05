---
title: Usare un servizio Web di Machine Learning da Excel | Microsoft Docs
description: Utilizzo di un servizio Web Azure Machine Learning da Excel | Azure
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: 9f1aac04d54221888ee9374317be339400dcf085
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="b3256-103">Utilizzo di un servizio Web Azure Machine Learning da Excel</span><span class="sxs-lookup"><span data-stu-id="b3256-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="b3256-104">Azure Machine Learning Studio semplifica la chiamata dei servizi Web direttamente da Excel senza dover di scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="b3256-104">Azure Machine Learning Studio makes it easy to call web services directly from Excel without the need to write any code.</span></span>

<span data-ttu-id="b3256-105">Se si usa Excel 2013 (o versione successiva) o Excel Online, è consigliabile usare il [componente aggiuntivo di Excel](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="b3256-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use the Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="b3256-106">Passi</span><span class="sxs-lookup"><span data-stu-id="b3256-106">Steps</span></span>
<span data-ttu-id="b3256-107">Pubblicazione di un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="b3256-107">Publish a web service.</span></span> <span data-ttu-id="b3256-108">[Questa pagina](machine-learning-walkthrough-5-publish-web-service.md) spiega come eseguire tale operazione.</span><span class="sxs-lookup"><span data-stu-id="b3256-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how to do it.</span></span> <span data-ttu-id="b3256-109">Attualmente la funzionalità della cartella di lavoro di Excel è supportata solo per i servizi di richiesta/risposta con un unico output cioè, una singola etichetta di valutazione.</span><span class="sxs-lookup"><span data-stu-id="b3256-109">Currently the Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="b3256-110">Dopo aver creato un servizio Web, fare clic sulla sezione **WEB SERVICES** sulla sinistra di Studio e quindi selezionare il servizio Web da utilizzare tramite Excel.</span><span class="sxs-lookup"><span data-stu-id="b3256-110">Once you have a web service, click on the **WEB SERVICES** section on the left of the studio, and then select the web service to consume from Excel.</span></span>

<span data-ttu-id="b3256-111">**Servizio Web classico**</span><span class="sxs-lookup"><span data-stu-id="b3256-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="b3256-112">Nella scheda **DASHBOARD** per il servizio Web è presente una riga per il servizio **REQUEST/RESPONSE**.</span><span class="sxs-lookup"><span data-stu-id="b3256-112">On the **DASHBOARD** tab for the web service is a row for the **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="b3256-113">Se il servizio ha un singolo output, è necessario vedere il collegamento **Download Excel Workbook** in quella riga.</span><span class="sxs-lookup"><span data-stu-id="b3256-113">If this service had a single output, you should see the **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="b3256-114">Fare clic su **Download Excel Workbook**(Scarica cartella di lavoro Excel).</span><span class="sxs-lookup"><span data-stu-id="b3256-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="b3256-115">**Nuovo servizio Web**</span><span class="sxs-lookup"><span data-stu-id="b3256-115">**New Web Service**</span></span>

1. <span data-ttu-id="b3256-116">Nel portale del servizio Web di Azure Machine Learning, selezionare **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="b3256-116">In the Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="b3256-117">Nella pagina Consume (Uso), nella sezione **Web service consumption options** (Opzioni d'uso del servizio Web) fare clic sull'icona di Excel.</span><span class="sxs-lookup"><span data-stu-id="b3256-117">On the Consume page, in the **Web service consumption options** section, click the Excel icon.</span></span>

<span data-ttu-id="b3256-118">**Uso della cartella di lavoro**</span><span class="sxs-lookup"><span data-stu-id="b3256-118">**Using the workbook**</span></span>

1. <span data-ttu-id="b3256-119">Aprire la cartella di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b3256-119">Open the workbook.</span></span>
2. <span data-ttu-id="b3256-120">Viene visualizzato un avviso di sicurezza. Fare clic sul pulsante **Abilita modifica**.</span><span class="sxs-lookup"><span data-stu-id="b3256-120">A Security Warning appears; click on the **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="b3256-121">Viene visualizzato un avviso di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="b3256-121">A Security Warning appears.</span></span> <span data-ttu-id="b3256-122">Fare clic sul pulsante **Abilita contenuto** per eseguire le macro nel foglio di calcolo.</span><span class="sxs-lookup"><span data-stu-id="b3256-122">Click on the **Enable Content** button to run macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="b3256-123">Una volta attivate le macro, viene generata una tabella.</span><span class="sxs-lookup"><span data-stu-id="b3256-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="b3256-124">Le colonne in blu sono necessarie come input nel servizio Web di richiesta-risposta (RRS) o **PARAMETRI**.</span><span class="sxs-lookup"><span data-stu-id="b3256-124">Columns in blue are required as input into the RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="b3256-125">Si noti che l'output del servizio RRS, **PREDICTED VALUES** è verde.</span><span class="sxs-lookup"><span data-stu-id="b3256-125">Note the output of the RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="b3256-126">Quando vengono riempite tutte le colonne per una determinata riga, la cartella di lavoro può automaticamente chiamare l'API di valutazione e visualizzare i risultati corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="b3256-126">When all columns for a given row are filled, the workbook automatically calls the scoring API, and displays the scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="b3256-127">Per valutare più di una riga, compilare la seconda riga con i dati, così verranno elaborati i valori stimati.</span><span class="sxs-lookup"><span data-stu-id="b3256-127">To score more than one row, fill the second row with data and the predicted values are produced.</span></span> <span data-ttu-id="b3256-128">È anche possibile incollare più righe contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="b3256-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="b3256-129">È possibile usare tutte le funzionalità di Excel (grafici, Power Map, formattazione condizionale e così via) con i valori stimati per visualizzare i dati.</span><span class="sxs-lookup"><span data-stu-id="b3256-129">You can use any of the Excel features (graphs, power map, conditional formatting, etc.) with the predicted values to help visualize the data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="b3256-130">Condivisione della cartella di lavoro</span><span class="sxs-lookup"><span data-stu-id="b3256-130">Sharing your workbook</span></span>
<span data-ttu-id="b3256-131">Affinché le macro funzionino, la chiave API deve far parte del foglio di calcolo.</span><span class="sxs-lookup"><span data-stu-id="b3256-131">For the macros to work, your API Key must be part of the spreadsheet.</span></span> <span data-ttu-id="b3256-132">Ciò significa che è necessario condividere la cartella di lavoro solo con le entità o i singoli utenti considerati attendibili.</span><span class="sxs-lookup"><span data-stu-id="b3256-132">That means that you should share the workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="b3256-133">Aggiornamenti automatici</span><span class="sxs-lookup"><span data-stu-id="b3256-133">Automatic updates</span></span>
<span data-ttu-id="b3256-134">Una chiamata RRS viene effettuata nei due casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b3256-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="b3256-135">La prima volta che una riga include contenuto in tutti i propri **PARAMETRI**</span><span class="sxs-lookup"><span data-stu-id="b3256-135">The first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="b3256-136">Ogni volta che uno dei **PARAMETRI** viene modificato in una riga che aveva tutti i **PARAMETRI** immessi.</span><span class="sxs-lookup"><span data-stu-id="b3256-136">Any time any of the **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
