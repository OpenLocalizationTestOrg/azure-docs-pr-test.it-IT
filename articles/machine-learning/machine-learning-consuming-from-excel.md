---
title: un servizio Web di Machine Learning da Excel aaaConsume | Documenti Microsoft
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
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a><span data-ttu-id="f55cc-103">Utilizzo di un servizio Web Azure Machine Learning da Excel</span><span class="sxs-lookup"><span data-stu-id="f55cc-103">Consuming an Azure Machine Learning Web Service from Excel</span></span>
 <span data-ttu-id="f55cc-104">Azure Machine Learning Studio rende facile toocall servizi web direttamente da Excel senza hello necessario toowrite qualsiasi codice.</span><span class="sxs-lookup"><span data-stu-id="f55cc-104">Azure Machine Learning Studio makes it easy toocall web services directly from Excel without hello need toowrite any code.</span></span>

<span data-ttu-id="f55cc-105">Se si utilizza Excel 2013 (o versioni successive) o Excel Online, si consiglia di utilizzare Excel hello [aggiuntivo di Excel](machine-learning-excel-add-in-for-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="f55cc-105">If you are using Excel 2013 (or later) or Excel Online, then we recommend that you use hello Excel [Excel add-in](machine-learning-excel-add-in-for-web-services.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a><span data-ttu-id="f55cc-106">Passi</span><span class="sxs-lookup"><span data-stu-id="f55cc-106">Steps</span></span>
<span data-ttu-id="f55cc-107">Pubblicazione di un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="f55cc-107">Publish a web service.</span></span> <span data-ttu-id="f55cc-108">[Questa pagina](machine-learning-walkthrough-5-publish-web-service.md) spiega come toodo è.</span><span class="sxs-lookup"><span data-stu-id="f55cc-108">[This page](machine-learning-walkthrough-5-publish-web-service.md) explains how toodo it.</span></span> <span data-ttu-id="f55cc-109">Funzionalità di cartella di lavoro di Excel hello è attualmente supportata solo per servizi di richiesta/risposta che dispongono di un singolo output (ovvero, un punteggio etichetta singola).</span><span class="sxs-lookup"><span data-stu-id="f55cc-109">Currently hello Excel workbook feature is only supported for Request/Response services that have a single output (that is, a single scoring label).</span></span> 

<span data-ttu-id="f55cc-110">Dopo aver creato un servizio web, fare clic su hello **servizi WEB** sezione sinistra hello di studio hello e quindi selezionare hello web servizio tooconsume da Excel.</span><span class="sxs-lookup"><span data-stu-id="f55cc-110">Once you have a web service, click on hello **WEB SERVICES** section on hello left of hello studio, and then select hello web service tooconsume from Excel.</span></span>

<span data-ttu-id="f55cc-111">**Servizio Web classico**</span><span class="sxs-lookup"><span data-stu-id="f55cc-111">**Classic Web Service**</span></span>

1. <span data-ttu-id="f55cc-112">In hello **DASHBOARD** scheda per il servizio web hello è una riga per hello **richiesta/risposta** servizio.</span><span class="sxs-lookup"><span data-stu-id="f55cc-112">On hello **DASHBOARD** tab for hello web service is a row for hello **REQUEST/RESPONSE** service.</span></span> <span data-ttu-id="f55cc-113">Se questo servizio dispone di un singolo output, dovrebbe essere hello **cartella di lavoro di Excel scaricare** collegamento in tale riga.</span><span class="sxs-lookup"><span data-stu-id="f55cc-113">If this service had a single output, you should see hello **Download Excel Workbook** link in that row.</span></span>
   
    ![][1]
2. <span data-ttu-id="f55cc-114">Fare clic su **Download Excel Workbook**(Scarica cartella di lavoro Excel).</span><span class="sxs-lookup"><span data-stu-id="f55cc-114">Click on **Download Excel Workbook**.</span></span>

<span data-ttu-id="f55cc-115">**Nuovo servizio Web**</span><span class="sxs-lookup"><span data-stu-id="f55cc-115">**New Web Service**</span></span>

1. <span data-ttu-id="f55cc-116">Nel portale del servizio Web di Azure Machine Learning hello, selezionare **consumare**.</span><span class="sxs-lookup"><span data-stu-id="f55cc-116">In hello Azure Machine Learning Web Service portal, select **Consume**.</span></span>
2. <span data-ttu-id="f55cc-117">Nella pagina di consumare, hello hello **opzioni di utilizzo del servizio Web** sezione fare clic sull'icona di Excel hello.</span><span class="sxs-lookup"><span data-stu-id="f55cc-117">On hello Consume page, in hello **Web service consumption options** section, click hello Excel icon.</span></span>

<span data-ttu-id="f55cc-118">**Utilizzare hello cartella di lavoro**</span><span class="sxs-lookup"><span data-stu-id="f55cc-118">**Using hello workbook**</span></span>

1. <span data-ttu-id="f55cc-119">Cartella di lavoro aperto hello.</span><span class="sxs-lookup"><span data-stu-id="f55cc-119">Open hello workbook.</span></span>
2. <span data-ttu-id="f55cc-120">Viene visualizzato un avviso di sicurezza; Fare clic su hello **Abilita modifica** pulsante.</span><span class="sxs-lookup"><span data-stu-id="f55cc-120">A Security Warning appears; click on hello **Enable Editing** button.</span></span>
   
    ![][2]
3. <span data-ttu-id="f55cc-121">Viene visualizzato un avviso di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f55cc-121">A Security Warning appears.</span></span> <span data-ttu-id="f55cc-122">Fare clic su hello **Abilita contenuto** pulsante toorun macro del foglio di calcolo.</span><span class="sxs-lookup"><span data-stu-id="f55cc-122">Click on hello **Enable Content** button toorun macros on your spreadsheet.</span></span>
   
    ![][3]
4. <span data-ttu-id="f55cc-123">Una volta attivate le macro, viene generata una tabella.</span><span class="sxs-lookup"><span data-stu-id="f55cc-123">Once macros are enabled, a table is generated.</span></span> <span data-ttu-id="f55cc-124">Le colonne sono blu richiesto come input per hello servizio web di record di risorse, o **parametri**.</span><span class="sxs-lookup"><span data-stu-id="f55cc-124">Columns in blue are required as input into hello RRS web service, or **PARAMETERS**.</span></span> <span data-ttu-id="f55cc-125">Notare l'output di hello di hello servizio RR, **PREDICTED VALUES** in verde.</span><span class="sxs-lookup"><span data-stu-id="f55cc-125">Note hello output of hello RRS service, **PREDICTED VALUES** in green.</span></span> <span data-ttu-id="f55cc-126">Quando tutte le colonne per una determinata riga sono riempite, cartella di lavoro hello automaticamente chiama l'API di punteggio hello e Visualizza risultati con punteggio hello.</span><span class="sxs-lookup"><span data-stu-id="f55cc-126">When all columns for a given row are filled, hello workbook automatically calls hello scoring API, and displays hello scored results.</span></span>
   
    ![][4]
5. <span data-ttu-id="f55cc-127">tooscore più di una riga, la seconda riga hello riempimento hello e dati stimati vengono prodotti i valori.</span><span class="sxs-lookup"><span data-stu-id="f55cc-127">tooscore more than one row, fill hello second row with data and hello predicted values are produced.</span></span> <span data-ttu-id="f55cc-128">È anche possibile incollare più righe contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="f55cc-128">You can even paste several rows at once.</span></span>

<span data-ttu-id="f55cc-129">È possibile utilizzare una delle caratteristiche di Excel hello (grafici, mappa power, condizionale formattazione e così via) con hello stimato valori toohelp visualizzare i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="f55cc-129">You can use any of hello Excel features (graphs, power map, conditional formatting, etc.) with hello predicted values toohelp visualize hello data.</span></span>    

## <a name="sharing-your-workbook"></a><span data-ttu-id="f55cc-130">Condivisione della cartella di lavoro</span><span class="sxs-lookup"><span data-stu-id="f55cc-130">Sharing your workbook</span></span>
<span data-ttu-id="f55cc-131">Per hello macro toowork, la chiave API deve essere parte del foglio di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="f55cc-131">For hello macros toowork, your API Key must be part of hello spreadsheet.</span></span> <span data-ttu-id="f55cc-132">Ciò significa che Condividi cartella di lavoro hello solo con le entità utenti singoli che è attendibile.</span><span class="sxs-lookup"><span data-stu-id="f55cc-132">That means that you should share hello workbook only with entities/individuals you trust.</span></span>

## <a name="automatic-updates"></a><span data-ttu-id="f55cc-133">Aggiornamenti automatici</span><span class="sxs-lookup"><span data-stu-id="f55cc-133">Automatic updates</span></span>
<span data-ttu-id="f55cc-134">Una chiamata RRS viene effettuata nei due casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="f55cc-134">An RRS call is made in these two situations:</span></span>

1. <span data-ttu-id="f55cc-135">Hello prima volta che una riga è contenuto in tutti i relativi **parametri**</span><span class="sxs-lookup"><span data-stu-id="f55cc-135">hello first time a row has content in all of its **PARAMETERS**</span></span>
2. <span data-ttu-id="f55cc-136">Ogni volta che uno qualsiasi dei hello **parametri** modifiche in una riga che contiene tutti i relativi **parametri** immesso.</span><span class="sxs-lookup"><span data-stu-id="f55cc-136">Any time any of hello **PARAMETERS** changes in a row that had all of its **PARAMETERS** entered.</span></span>

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
