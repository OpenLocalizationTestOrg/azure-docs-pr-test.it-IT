---
title: Componente aggiuntivo di Excel per i servizi Web di Machine Learning | Documentazione Microsoft
description: Come usare i servizi Web di Azure Machine Learning direttamente in Excel senza scrivere codice.
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
ms.openlocfilehash: 0d60dd87bbdd4d3eafac0f8876cc9e41412a53ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="excel-add-in-for-azure-machine-learning-web-services"></a><span data-ttu-id="dfe6e-103">Componente aggiuntivo Excel per i servizi Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="dfe6e-103">Excel Add-in for Azure Machine Learning web services</span></span>
<span data-ttu-id="dfe6e-104">Excel consente di chiamare servizi Web direttamente senza dover scrivere alcun codice.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-104">Excel makes it easy to call web services directly without the need to write any code.</span></span>

## <a name="steps-to-use-an-existing-web-service-in-the-workbook"></a><span data-ttu-id="dfe6e-105">Procedura per usare un servizio Web esistente nella cartella di lavoro</span><span class="sxs-lookup"><span data-stu-id="dfe6e-105">Steps to Use an Existing web service in the Workbook</span></span>

1. <span data-ttu-id="dfe6e-106">Aprire il [file di Excel di esempio](http://aka.ms/amlexcel-sample-2)che contiene il componente aggiuntivo Excel e i dati relativi ai passeggeri sul Titanic.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-106">Open the [sample Excel file](http://aka.ms/amlexcel-sample-2), which contains the Excel add-in and data about passengers on the Titanic.</span></span>
2. <span data-ttu-id="dfe6e-107">Scegliere un servizio Web facendo clic su di esso: in questo esempio "Stime sopravvissuti Titanic (esempio componente aggiuntivo Excel) [Score]".</span><span class="sxs-lookup"><span data-stu-id="dfe6e-107">Choose the web service by clicking it - "Titanic Survivor Predictor (Excel Add-in Sample) [Score]" in this example.</span></span>
   
    ![Selezionare il servizio Web][01]
3. <span data-ttu-id="dfe6e-109">Viene visualizzata la sezione **Stima**.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-109">This takes you to the **Predict** section.</span></span>  <span data-ttu-id="dfe6e-110">Questa cartella di lavoro contiene già dati di esempio, ma per una cartella di lavoro vuota è anche possibile selezionare una cella in Excel e fare clic su **Use sample data**(Usa dati di esempio).</span><span class="sxs-lookup"><span data-stu-id="dfe6e-110">This workbook already contains sample data, but for a blank workbook you can select a cell in Excel and click **Use sample data**.</span></span>
4. <span data-ttu-id="dfe6e-111">Selezionare i dati con intestazioni e fare clic sull'icona dell'intervallo dei dati di input.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-111">Select the data with headers and click the input data range icon.</span></span>  <span data-ttu-id="dfe6e-112">Assicurarsi che sia selezionata la casella "Dati con intestazioni".</span><span class="sxs-lookup"><span data-stu-id="dfe6e-112">Make sure the "My data has headers" box is checked.</span></span>
5. <span data-ttu-id="dfe6e-113">In **Output** immettere il numero di cella in cui si vuole inserire l'output, in questo caso ad esempio "H1".</span><span class="sxs-lookup"><span data-stu-id="dfe6e-113">Under **Output**, enter the cell number where you want the output to be, for example "H1" here.</span></span>
6. <span data-ttu-id="dfe6e-114">Fare clic su **Stima**.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-114">Click **Predict**.</span></span>
   
    ![Sezione Stima][02]

<span data-ttu-id="dfe6e-116">Distribuire un servizio Web o usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-116">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="dfe6e-117">Per altre informazioni sulla distribuzione di un servizio Web, vedere [Passaggio 5 della procedura dettagliata: Distribuire il servizio Web di Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="dfe6e-117">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

<span data-ttu-id="dfe6e-118">Ottenere la chiave API per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-118">Get the API key for your web service.</span></span> <span data-ttu-id="dfe6e-119">La posizione in cui viene eseguita l'operazione varia a seconda che sia stato pubblicato un servizio Web classico o un nuovo servizio Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-119">Where you perform this action depends on whether you published a Classic Machine Learning web service of a New Machine Learning web service.</span></span>

<span data-ttu-id="dfe6e-120">**Usare un servizio Web classico**</span><span class="sxs-lookup"><span data-stu-id="dfe6e-120">**Use a Classic web service**</span></span> 

1. <span data-ttu-id="dfe6e-121">In Machine Learning Studio fare clic sulla sezione **SERVIZI WEB** sulla sinistra e quindi selezionare il servizio Web da usare.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-121">In Machine Learning Studio, click the **WEB SERVICES** section in the left pane, and then select the web service.</span></span>
   
    ![Selezione di un servizio Web in Studio][04]
2. <span data-ttu-id="dfe6e-123">Copiare la chiave dell'API per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-123">Copy the API key for the web service.</span></span>
   
    ![Chiave API in Studio][05]
3. <span data-ttu-id="dfe6e-125">Nella scheda **DASHBOARD** per il servizio Web fare clic sul collegamento **RICHIESTA/RISPOSTA**.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-125">On the **DASHBOARD** tab for the web service, click the **REQUEST/RESPONSE** link.</span></span>
4. <span data-ttu-id="dfe6e-126">Cercare la sezione **Request URI** (Richiedi URI).</span><span class="sxs-lookup"><span data-stu-id="dfe6e-126">Look for the **Request URI** section.</span></span>  <span data-ttu-id="dfe6e-127">Copiare e salvare l'URL.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-127">Copy and save the URL.</span></span>

> [!NOTE]
> <span data-ttu-id="dfe6e-128">È ora possibile accedere al [portale dei servizi Web di Azure Machine Learning](https://services.azureml.net) per ottenere la chiave API per un servizio Web classico di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-128">It is now possible to sign into the [Azure Machine Learning Web Services](https://services.azureml.net) portal to obtain the API key for a Classic Machine Learning web service.</span></span>
> 
> 

<span data-ttu-id="dfe6e-129">**Usare un nuovo servizio Web**</span><span class="sxs-lookup"><span data-stu-id="dfe6e-129">**Use a New web service**</span></span>

1. <span data-ttu-id="dfe6e-130">Nel [portale dei servizi Web di Azure Machine Learning](https://services.azureml.net) fare clic su **Servizi Web**, poi selezionare il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-130">In the [Azure Machine Learning Web Services](https://services.azureml.net) portal, click **Web Services**, then select your web service.</span></span> 
2. <span data-ttu-id="dfe6e-131">Fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="dfe6e-131">Click **Consume**.</span></span>
3. <span data-ttu-id="dfe6e-132">Cercare la sezione **Basic consumption info** (Informazioni di base sull'uso).</span><span class="sxs-lookup"><span data-stu-id="dfe6e-132">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="dfe6e-133">Copiare e salvare il valore di **Primary Key** (Chiave primaria) e l'URL **Request-Response** (Richiesta-risposta).</span><span class="sxs-lookup"><span data-stu-id="dfe6e-133">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>

## <a name="steps-to-add-a-new-web-service"></a><span data-ttu-id="dfe6e-134">Procedura per aggiungere un nuovo servizio Web</span><span class="sxs-lookup"><span data-stu-id="dfe6e-134">Steps to Add a New web service</span></span>

1. <span data-ttu-id="dfe6e-135">Distribuire un servizio Web o usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-135">Deploy a web service or use an existing Web service.</span></span> <span data-ttu-id="dfe6e-136">Per altre informazioni sulla distribuzione di un servizio Web, vedere [Passaggio 5 della procedura dettagliata: Distribuire il servizio Web di Machine Learning](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="dfe6e-136">For more information on deploying a web service, see [Walkthrough Step 5: Deploy the Azure Machine Learning Web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
2. <span data-ttu-id="dfe6e-137">Fare clic su **Consume**(Uso).</span><span class="sxs-lookup"><span data-stu-id="dfe6e-137">Click **Consume**.</span></span>
3. <span data-ttu-id="dfe6e-138">Cercare la sezione **Basic consumption info** (Informazioni di base sull'uso).</span><span class="sxs-lookup"><span data-stu-id="dfe6e-138">Look for the **Basic consumption info** section.</span></span> <span data-ttu-id="dfe6e-139">Copiare e salvare il valore di **Primary Key** (Chiave primaria) e l'URL **Request-Response** (Richiesta-risposta).</span><span class="sxs-lookup"><span data-stu-id="dfe6e-139">Copy and save the **Primary Key** and the **Request-Response** URL.</span></span>
4. <span data-ttu-id="dfe6e-140">In Excel passare alla sezione **Servizi Web** (se si è nella sezione **Stima**, fare clic sulla freccia indietro per tornare all'elenco dei servizi Web).</span><span class="sxs-lookup"><span data-stu-id="dfe6e-140">In Excel, go to the **Web Services** section (if you are in the **Predict** section, click the back arrow to go to the list of web services).</span></span>
   
    ![Passare alla selezione del servizio Web][03]
5. <span data-ttu-id="dfe6e-142">Fare clic su **Aggiungi servizio Web**.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-142">Click **Add Web Service**.</span></span>
6. <span data-ttu-id="dfe6e-143">Incollare l'URL nella casella di testo **URL**del componente aggiuntivo Excel.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-143">Paste the URL into the Excel add-in text box labeled **URL**.</span></span>
7. <span data-ttu-id="dfe6e-144">Incollare la chiave API/primaria nella casella di testo **Chiave API**.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-144">Paste the API/Primary key into the text box labeled **API key**.</span></span>
8. <span data-ttu-id="dfe6e-145">Fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-145">Click **Add**.</span></span>
   
    ![URL e chiave API per un servizio Web classico.][06]
9. <span data-ttu-id="dfe6e-147">Per usare il servizio Web, seguire le indicazioni illustrate in precedenza nella sezione "Procedura per usare un servizio Web esistente".</span><span class="sxs-lookup"><span data-stu-id="dfe6e-147">To use the web service, follow the preceding directions, "Steps to Use an Existing web Service."</span></span>

## <a name="sharing-your-workbook"></a><span data-ttu-id="dfe6e-148">Condivisione della cartella di lavoro</span><span class="sxs-lookup"><span data-stu-id="dfe6e-148">Sharing Your Workbook</span></span>
<span data-ttu-id="dfe6e-149">Se si salva la cartella di lavoro, verrà salvata anche la chiave API/primaria per i servizi Web che sono stati aggiunti.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-149">If you save your workbook, then the API/Primary key for the web services you have added is also saved.</span></span> <span data-ttu-id="dfe6e-150">Pertanto, è necessario condividere la cartella di lavoro solo con persone attendibili.</span><span class="sxs-lookup"><span data-stu-id="dfe6e-150">That means you should only share the workbook with individuals you trust.</span></span>

<span data-ttu-id="dfe6e-151">In caso di domande, inserirle nella sezione seguente dedicata ai commenti o nel [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="dfe6e-151">Ask any questions in the following comment section or on our [forum](http://go.microsoft.com/fwlink/?LinkID=403669&clcid=0x409).</span></span>

[01]: ./media/machine-learning-excel-add-in-for-web-services/image1.png
[02]: ./media/machine-learning-excel-add-in-for-web-services/image2.png
[03]: ./media/machine-learning-excel-add-in-for-web-services/image3.png
[04]: ./media/machine-learning-excel-add-in-for-web-services/image4.png
[05]: ./media/machine-learning-excel-add-in-for-web-services/image5.png
[06]: ./media/machine-learning-excel-add-in-for-web-services/image6.png
