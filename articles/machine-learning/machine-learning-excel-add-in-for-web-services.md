---
title: il componente aggiuntivo aaaExcel per i servizi Web di Machine Learning | Documenti Microsoft
description: Come toouse Web di Azure Machine Learning services direttamente in Excel senza scrivere alcun codice.
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 9618079d-502f-4974-a3e2-8f924042a23f
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/14/2017
ms.author: tedway;garye
ms.openlocfilehash: c52f40d33c9907f284e4750afe47181dc3365fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="369d7-103">Componente aggiuntivo Excel per i servizi Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="369d7-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="369d7-104">Excel rende facile toocall i servizi web direttamente senza hello necessario toowrite qualsiasi codice.</span><span class="sxs-lookup"><span data-stu-id="369d7-104">Excel makes it easy toocall web services directly without hello need toowrite any code.</span></span>

## <a name="steps-toouse-an-existing-web-service-in-hello-workbook"></a><span data-ttu-id="369d7-105">Passaggi tooUse un servizio web esistente nella cartella di lavoro hello</span><span class="sxs-lookup"><span data-stu-id="369d7-105">Steps tooUse an Existing web service in hello Workbook</span></span>

1. <span data-ttu-id="369d7-106">Aprire hello [file di Excel di esempio](http://aka.ms/amlexcel-sample-2), che contiene hello aggiuntivo Excel e dati sul passeggeri in hello Titanic.</span><span class="sxs-lookup"><span data-stu-id="369d7-106">Open hello [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains hello Excel add-in and data about passengers on hello Titanic.</span></span>
2. <span data-ttu-id="369d7-107">Scegliere servizio web hello facendovi clic sopra-"Titanic superstite predittive (componente aggiuntivo di Excel esempio) [punteggio]" in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="369d7-107">Choose hello web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Selezionare il servizio Web][01]
3. <span data-ttu-id="369d7-109">Consente di passare toohello **Predict** sezione.</span><span class="sxs-lookup"><span data-stu-id="369d7-109">This takes you toohello **Predict** section.</span></span>  <span data-ttu-id="369d7-110">Questa cartella di lavoro contiene già dati di esempio, ma per una cartella di lavoro vuota è anche possibile selezionare una cella in Excel e fare clic su **Use sample data**(Usa dati di esempio).</span><span class="sxs-lookup"><span data-stu-id="369d7-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="369d7-111">Selezionare i dati di hello con intestazioni e fare clic sull'icona di intervallo di hello dati di input.</span><span class="sxs-lookup"><span data-stu-id="369d7-111">Select hello data with headers and click hello input data range icon.</span></span>  <span data-ttu-id="369d7-112">Verificare che sia selezionata la casella "dati con intestazioni" hello.</span><span class="sxs-lookup"><span data-stu-id="369d7-112">Make sure hello "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="369d7-113">In **Output**, immettere il numero di celle hello in cui si desidera hello toobe output, ad esempio "H1" di seguito.</span><span class="sxs-lookup"><span data-stu-id="369d7-113">Under **Output**, enter hello cell number where you want hello output toobe, for example "H1" here.</span></span>
6. <span data-ttu-id="369d7-114">Fare clic su **Stima**.</span><span class="sxs-lookup"><span data-stu-id="369d7-114">Click **Predict**.</span></span>
   
    ![Sezione Stima][02]

<span data-ttu-id="369d7-116">Distribuire un servizio Web o usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="369d7-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="369d7-117">Per ulteriori informazioni sulla distribuzione di un servizio web, vedere [passaggio 5 di questa procedura dettagliata: distribuzione di servizio Web di Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="369d7-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="369d7-118">Ottenere la chiave API hello per il servizio web.</span><span class="sxs-lookup"><span data-stu-id="369d7-118">Get hello API key for your web service.</span></span> <span data-ttu-id="369d7-119">La posizione in cui viene eseguita l'operazione varia a seconda che sia stato pubblicato un servizio Web classico o un nuovo servizio Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="369d7-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="369d7-120">**Usare un servizio Web classico**</span><span class="sxs-lookup"><span data-stu-id="369d7-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="369d7-121">In Machine Learning Studio, fare clic su hello **servizi WEB** sezione nel riquadro di sinistra hello e quindi selezionare servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="369d7-121">In Machine Learning Studio, click hello **WEB SERVICES** section in hello left pane, and then select hello web service.</span></span>
   
    ![Selezione di un servizio Web in Studio][04]
2. <span data-ttu-id="369d7-123">Copiare la chiave API hello per il servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="369d7-123">Copy hello API key for hello web service.</span></span>
   
    ![Chiave API in Studio][05]
3. <span data-ttu-id="369d7-125">In hello **DASHBOARD** per servizio web hello scheda, fare clic su hello **richiesta/risposta** collegamento.</span><span class="sxs-lookup"><span data-stu-id="369d7-125">On hello **DASHBOARD** tab for hello web service, click hello **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="369d7-126">Cercare hello **URI della richiesta** sezione.</span><span class="sxs-lookup"><span data-stu-id="369d7-126">Look for hello **Request URI** section.</span></span>  <span data-ttu-id="369d7-127">Copiare e salvare hello URL.</span><span class="sxs-lookup"><span data-stu-id="369d7-127">Copy and save hello URL.</span></span>

> [!NOTE]
> <span data-ttu-id="369d7-128">È ora possibile toosign in hello [servizi Web di Azure Machine Learning](https://services.azureml.net) chiave hello API tooobtain portale per un servizio web classico Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="369d7-128">It is now possible toosign into hello [Azure Machine Learning Web Services](https://services.azureml.net) portal tooobtain hello API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="369d7-129">**Usare un nuovo servizio Web**</span><span class="sxs-lookup"><span data-stu-id="369d7-129">**Use a New web service**</span></span>

1. <span data-ttu-id="369d7-130">In hello [servizi Web di Azure Machine Learning](https://services.azureml.net) portale, fare clic su **servizi Web**, quindi selezionare il servizio web.</span><span class="sxs-lookup"><span data-stu-id="369d7-130">In hello [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="369d7-131">Fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="369d7-131">Click **Consume**.</span></span>
3. <span data-ttu-id="369d7-132">Cercare hello **informazioni di base al consumo** sezione.</span><span class="sxs-lookup"><span data-stu-id="369d7-132">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="369d7-133">Copiare e salvare hello **chiave primaria** hello e **richiesta-risposta** URL.</span><span class="sxs-lookup"><span data-stu-id="369d7-133">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>

## <a name="steps-tooadd-a-new-web-service"></a><span data-ttu-id="369d7-134">Passaggi tooAdd un nuovo servizio web</span><span class="sxs-lookup"><span data-stu-id="369d7-134">Steps tooAdd a New web service</span></span>

1. <span data-ttu-id="369d7-135">Distribuire un servizio Web o usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="369d7-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="369d7-136">Per ulteriori informazioni sulla distribuzione di un servizio web, vedere [passaggio 5 di questa procedura dettagliata: distribuzione di servizio Web di Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="369d7-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy hello Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="369d7-137">Fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="369d7-137">Click **Consume**.</span></span>
3. <span data-ttu-id="369d7-138">Cercare hello **informazioni di base al consumo** sezione.</span><span class="sxs-lookup"><span data-stu-id="369d7-138">Look for hello **Basic consumption info** section.</span></span> <span data-ttu-id="369d7-139">Copiare e salvare hello **chiave primaria** hello e **richiesta-risposta** URL.</span><span class="sxs-lookup"><span data-stu-id="369d7-139">Copy and save hello **Primary Key** and hello **Request-Response** URL.</span></span>
4. <span data-ttu-id="369d7-140">In Excel, visitare toohello **servizi Web** sezione (in hello **Predict** sezione, fare clic su hello freccia indietro toogo toohello elenco dei servizi web).</span><span class="sxs-lookup"><span data-stu-id="369d7-140">In Excel, go toohello **Web Services** section (if you are in hello **Predict** section, click hello back arrow toogo toohello list of web services).</span></span>
   
    ![Passare la selezione di servizio tooWeb][03]
5. <span data-ttu-id="369d7-142">Fare clic su **Aggiungi servizio Web**.</span><span class="sxs-lookup"><span data-stu-id="369d7-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="369d7-143">Incollare hello URL nella casella di testo di componente aggiuntivo di Excel hello **URL**.</span><span class="sxs-lookup"><span data-stu-id="369d7-143">Paste hello URL into hello Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="369d7-144">Chiave API o primario di hello Incolla nella casella di testo hello **chiave API**.</span><span class="sxs-lookup"><span data-stu-id="369d7-144">Paste hello API/Primary key into hello text box labeled **API key**.</span></span>
8. <span data-ttu-id="369d7-145">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="369d7-145">Click **Add**.</span></span>
   
    ![URL e chiave API per un servizio Web classico.][06]
9. <span data-ttu-id="369d7-147">servizio web di hello toouse, hello precedono le direzioni, consultare "Passaggi tooUse un servizio web di esistente."</span><span class="sxs-lookup"><span data-stu-id="369d7-147">toouse hello web service, follow hello preceding directions, "Steps tooUse an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="369d7-148">Condivisione della cartella di lavoro</span><span class="sxs-lookup"><span data-stu-id="369d7-148">Sharing Your Workbook</span></span>
<span data-ttu-id="369d7-149">Se si salva la cartella di lavoro, viene salvata anche chiave API o primario hello per servizi web hello che è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="369d7-149">If you save your workbook, then hello API/Primary key for hello web services you have added is also saved.</span></span> <span data-ttu-id="369d7-150">Pertanto, che si deve solo condivisione hello con utenti che attendibili.</span><span class="sxs-lookup"><span data-stu-id="369d7-150">That means you should only share hello workbook with individuals you trust.</span></span>

<span data-ttu-id="369d7-151">Porre domande in hello seguenti commento sezione o nella nostri [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="369d7-151">Ask any questions in hello following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
