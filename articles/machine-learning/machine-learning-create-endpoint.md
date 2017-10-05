---
title: Creazione di endpoint del servizio Web in Machine Learning | Documentazione Microsoft
description: Creazione di endpoint del servizio Web in Azure Machine Learning
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 9f83ffc9cf7dbe37c1ce9980fd7f5b9133fe78f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="7cce7-103">Creazione di endpoint</span><span class="sxs-lookup"><span data-stu-id="7cce7-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="7cce7-104">Questo argomento descrive le tecniche applicabili a un servizio Web di Machine Learning **classico**.</span><span class="sxs-lookup"><span data-stu-id="7cce7-104">This topic describes techniques applicable to a **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="7cce7-105">Quando si creano servizi Web da vendere ai propri clienti, è necessario fornire dei modelli con training per ogni cliente che sono ancora collegati all'esperimento da cui è stato creato il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="7cce7-105">When you create Web services that you sell forward to your customers, you need to provide trained models to each customer that are still linked to the experiment from which the Web service was created.</span></span> <span data-ttu-id="7cce7-106">Inoltre, qualsiasi aggiornamento all'esperimento deve essere applicato in maniera selettiva a un endpoint, senza sovrascrivere le personalizzazioni.</span><span class="sxs-lookup"><span data-stu-id="7cce7-106">In addition, any updates to the experiment should be applied selectively to an endpoint without overwriting the customizations.</span></span>

<span data-ttu-id="7cce7-107">Per farlo, Azure Machine Learning consente di creare più endpoint per un servizio Web distribuito.</span><span class="sxs-lookup"><span data-stu-id="7cce7-107">To accomplish this, Azure Machine Learning allows you to create multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="7cce7-108">Ciascun endpoint nel servizio Web viene indirizzato, limitato e gestito in maniera indipendente.</span><span class="sxs-lookup"><span data-stu-id="7cce7-108">Each endpoint in the Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="7cce7-109">Ciascun endpoint rappresnta un URL univoco e una chiave di autorizzazione che è possibile distribuire ai clienti.</span><span class="sxs-lookup"><span data-stu-id="7cce7-109">Each endpoint is a unique URL and authorization key that you can distribute to your customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-to-a-web-service"></a><span data-ttu-id="7cce7-110">Aggiunta di endpoint a un servizio Web</span><span class="sxs-lookup"><span data-stu-id="7cce7-110">Adding endpoints to a Web service</span></span>
<span data-ttu-id="7cce7-111">Esistono tre modi per aggiungere un endpoint a un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="7cce7-111">There are three ways to add an endpoint to a Web service.</span></span>

* <span data-ttu-id="7cce7-112">A livello di codice</span><span class="sxs-lookup"><span data-stu-id="7cce7-112">Programmatically</span></span>
* <span data-ttu-id="7cce7-113">Mediante il portale dei servizi Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7cce7-113">Through the Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="7cce7-114">Mediante il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="7cce7-114">Though the Azure classic portal</span></span>

<span data-ttu-id="7cce7-115">Dopo aver creato l'endpoint, è possibile utilizzarlo tramite le API sincrone, le API batch e i fogli di lavoro di Excel.</span><span class="sxs-lookup"><span data-stu-id="7cce7-115">Once the endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="7cce7-116">Oltre ad aggiungere gli endpoint tramite questa interfaccia, è possibile utilizzare anche le API di gestione Endpoint a livello di codice aggiungere gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="7cce7-116">In addition to adding endpoints through this UI, you can also use the Endpoint Management APIs to programmatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="7cce7-117">Se sono stati aggiunti altri endpoint al servizio Web, non è possibile eliminare l'endpoint predefinito.</span><span class="sxs-lookup"><span data-stu-id="7cce7-117">If you have added additional endpoints to the Web service, you cannot delete the default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="7cce7-118">Aggiunta di un endpoint a livello di codice</span><span class="sxs-lookup"><span data-stu-id="7cce7-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="7cce7-119">È possibile aggiungere un endpoint al servizio Web a livello di codice mediante il codice di esempio [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="7cce7-119">You can add an endpoint to your Web service programmatically using the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="7cce7-120">Aggiunta di un endpoint mediante il portale dei servizi Web di Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="7cce7-120">Adding an endpoint using the Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="7cce7-121">In Machine Learning Studio fare clic su Web Services (Servizi Web) nella colonna di spostamento a sinistra.</span><span class="sxs-lookup"><span data-stu-id="7cce7-121">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="7cce7-122">Nella parte inferiore del dashboard dei servizi Web, fare clic su **Gestisci endpoint**.</span><span class="sxs-lookup"><span data-stu-id="7cce7-122">At the bottom of the Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="7cce7-123">Nel portale dei servizi Web di Azure Machine Learning viene visualizzata la pagina dedicata agli endpoint del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="7cce7-123">The Azure Machine Learning Web Services portal opens to the endpoints page for the Web service.</span></span>
3. <span data-ttu-id="7cce7-124">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="7cce7-124">Click **New**.</span></span>
4. <span data-ttu-id="7cce7-125">Immettere un nome e una descrizione per il nuovo endpoint.</span><span class="sxs-lookup"><span data-stu-id="7cce7-125">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="7cce7-126">I nomi degli endpoint devono contenere al massimo 24 caratteri alfanumerici (con lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="7cce7-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="7cce7-127">Selezionare il livello di registrazione e indicare se i dati di esempio sono abilitati.</span><span class="sxs-lookup"><span data-stu-id="7cce7-127">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="7cce7-128">Per altre informazioni sulla registrazione, vedere [Abilitare la registrazione per i servizi Web di Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="7cce7-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-the-azure-classic-portal"></a><span data-ttu-id="7cce7-129">Aggiunta di un endpoint usando il portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="7cce7-129">Adding an endpoint using the Azure classic portal</span></span>
1. <span data-ttu-id="7cce7-130">Accedere al [portale di Azure classico](http://manage.windowsazure.com), fare clic su **Machine Learning** nella colonna sinistra.</span><span class="sxs-lookup"><span data-stu-id="7cce7-130">Sign in to the [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in the left column.</span></span> <span data-ttu-id="7cce7-131">Fare clic sull'area di lavoro che contiene il servizio Web a cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="7cce7-131">Click the workspace which contains the Web service in which you are interested.</span></span>
   
    ![Passare all'area di lavoro](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="7cce7-133">Fare clic su **Servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="7cce7-133">Click **Web Services**.</span></span>
   
    ![Passare ai servizi Web](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="7cce7-135">Fare clic sul servizio Web a cui si è interessati per visualizzare l'elenco degli endpoint disponibili.</span><span class="sxs-lookup"><span data-stu-id="7cce7-135">Click the Web service you're interested in to see the list of available endpoints.</span></span>
   
    ![Passare all'endpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="7cce7-137">Nella parte inferiore della pagina fare clic su **Aggiungi endpoint**.</span><span class="sxs-lookup"><span data-stu-id="7cce7-137">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="7cce7-138">Inserire un nome e una descrizione, assicurarsi che non siano presenti altri endpoint con lo stesso nome nel servizio Web.</span><span class="sxs-lookup"><span data-stu-id="7cce7-138">Type a name and description, ensure there are no other endpoints with the same name in this Web service.</span></span> <span data-ttu-id="7cce7-139">Lasciare il livello di limitazione con il valore predefinito, a meno di avere esigenze particolari.</span><span class="sxs-lookup"><span data-stu-id="7cce7-139">Leave the throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="7cce7-140">Per altre informazioni sulle limitazioni, vedere [Ridimensionamento degli endpoint dell'API](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="7cce7-140">To learn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Creare un endpoint](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="7cce7-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7cce7-142">Next Steps</span></span>
<span data-ttu-id="7cce7-143">[Come usare un servizio Web di Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="7cce7-143">[How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

