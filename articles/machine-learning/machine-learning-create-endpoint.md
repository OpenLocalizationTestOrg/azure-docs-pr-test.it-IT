---
title: endpoint del servizio Web aaaCreating in Machine Learning | Documenti Microsoft
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
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a><span data-ttu-id="35af6-103">Creazione di endpoint</span><span class="sxs-lookup"><span data-stu-id="35af6-103">Creating Endpoints</span></span>
> [!NOTE]
>  <span data-ttu-id="35af6-104">Questo argomento vengono descritte le tecniche applicabile tooa **classico** servizio Web di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="35af6-104">This topic describes techniques applicable tooa **Classic** Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="35af6-105">Quando si creano servizi Web che si vendono tooyour Avanti clienti, è necessario cliente tooeach di modelli di training tooprovide che sono ancora collegato toohello esperimento da quale hello Web servizio è stato creato.</span><span class="sxs-lookup"><span data-stu-id="35af6-105">When you create Web services that you sell forward tooyour customers, you need tooprovide trained models tooeach customer that are still linked toohello experiment from which hello Web service was created.</span></span> <span data-ttu-id="35af6-106">Inoltre, gli aggiornamenti toohello esperimento deve essere applicati in modo selettivo tooan endpoint senza sovrascrivere le personalizzazioni hello.</span><span class="sxs-lookup"><span data-stu-id="35af6-106">In addition, any updates toohello experiment should be applied selectively tooan endpoint without overwriting hello customizations.</span></span>

<span data-ttu-id="35af6-107">tooaccomplish, Azure Machine Learning consente toocreate più endpoint per un servizio Web distribuito.</span><span class="sxs-lookup"><span data-stu-id="35af6-107">tooaccomplish this, Azure Machine Learning allows you toocreate multiple endpoints for a deployed Web service.</span></span> <span data-ttu-id="35af6-108">Ogni endpoint nel servizio Web hello in modo indipendente è indirizzata, limitata e gestito.</span><span class="sxs-lookup"><span data-stu-id="35af6-108">Each endpoint in hello Web service is independently addressed, throttled, and managed.</span></span> <span data-ttu-id="35af6-109">Ogni endpoint è una chiave univoca di URL e l'autorizzazione che è possibile distribuire i clienti tooyour.</span><span class="sxs-lookup"><span data-stu-id="35af6-109">Each endpoint is a unique URL and authorization key that you can distribute tooyour customers.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a><span data-ttu-id="35af6-110">Aggiunta del servizio Web di endpoint tooa</span><span class="sxs-lookup"><span data-stu-id="35af6-110">Adding endpoints tooa Web service</span></span>
<span data-ttu-id="35af6-111">Esistono tre modi tooadd un tooa endpoint servizio Web.</span><span class="sxs-lookup"><span data-stu-id="35af6-111">There are three ways tooadd an endpoint tooa Web service.</span></span>

* <span data-ttu-id="35af6-112">A livello di codice</span><span class="sxs-lookup"><span data-stu-id="35af6-112">Programmatically</span></span>
* <span data-ttu-id="35af6-113">Tramite il portale di servizi Web di Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="35af6-113">Through hello Azure Machine Learning Web Services portal</span></span>
* <span data-ttu-id="35af6-114">Sebbene hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="35af6-114">Though hello Azure classic portal</span></span>

<span data-ttu-id="35af6-115">Dopo aver creato endpoint hello, è possibile utilizzarlo tramite le API sincrone, le API, batch e fogli di lavoro di excel.</span><span class="sxs-lookup"><span data-stu-id="35af6-115">Once hello endpoint is created, you can consume it through synchronous APIs, batch APIs, and excel worksheets.</span></span> <span data-ttu-id="35af6-116">Inoltre tooadding endpoint tramite questa interfaccia, è inoltre possibile utilizzare hello API di gestione Endpoint tooprogrammatically aggiungere gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="35af6-116">In addition tooadding endpoints through this UI, you can also use hello Endpoint Management APIs tooprogrammatically add endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="35af6-117">Se sono stati aggiunti toohello altri endpoint servizio Web, è possibile eliminare l'endpoint predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="35af6-117">If you have added additional endpoints toohello Web service, you cannot delete hello default endpoint.</span></span>
> 
> 

## <a name="adding-an-endpoint-programmatically"></a><span data-ttu-id="35af6-118">Aggiunta di un endpoint a livello di codice</span><span class="sxs-lookup"><span data-stu-id="35af6-118">Adding an endpoint programmatically</span></span>
<span data-ttu-id="35af6-119">È possibile aggiungere un servizio Web di tooyour endpoint a livello di programmazione utilizzando hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) codice di esempio.</span><span class="sxs-lookup"><span data-stu-id="35af6-119">You can add an endpoint tooyour Web service programmatically using hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a><span data-ttu-id="35af6-120">Aggiunta di un endpoint tramite il portale di servizi Web di Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="35af6-120">Adding an endpoint using hello Azure Machine Learning Web Services portal</span></span>
1. <span data-ttu-id="35af6-121">In Machine Learning Studio, nella colonna sinistra hello, fare clic su servizi Web.</span><span class="sxs-lookup"><span data-stu-id="35af6-121">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="35af6-122">Nella parte inferiore di hello del dashboard del servizio Web hello, fare clic su **gestire endpoint**.</span><span class="sxs-lookup"><span data-stu-id="35af6-122">At hello bottom of hello Web service dashboard, click **Manage endpoints**.</span></span> <span data-ttu-id="35af6-123">pagina endpoint toohello per hello servizio Web viene visualizzato il portale di servizi Web di Azure Machine Learning Hello.</span><span class="sxs-lookup"><span data-stu-id="35af6-123">hello Azure Machine Learning Web Services portal opens toohello endpoints page for hello Web service.</span></span>
3. <span data-ttu-id="35af6-124">Fare clic su **New**.</span><span class="sxs-lookup"><span data-stu-id="35af6-124">Click **New**.</span></span>
4. <span data-ttu-id="35af6-125">Digitare un nome e una descrizione per il nuovo endpoint di hello.</span><span class="sxs-lookup"><span data-stu-id="35af6-125">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="35af6-126">I nomi degli endpoint devono contenere al massimo 24 caratteri alfanumerici (con lettere minuscole).</span><span class="sxs-lookup"><span data-stu-id="35af6-126">Endpoint names must be 24 character or less in length, and must be made up of lower-case alphabets or numbers.</span></span> <span data-ttu-id="35af6-127">Selezionare il livello di registrazione hello e indica se sono abilitati i dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="35af6-127">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="35af6-128">Per altre informazioni sulla registrazione, vedere [Abilitare la registrazione per i servizi Web di Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="35af6-128">For more information on logging, see [Enable logging for Machine Learning Web services](machine-learning-web-services-logging.md).</span></span>

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a><span data-ttu-id="35af6-129">Aggiunta di un endpoint utilizzando hello portale di Azure classico</span><span class="sxs-lookup"><span data-stu-id="35af6-129">Adding an endpoint using hello Azure classic portal</span></span>
1. <span data-ttu-id="35af6-130">Accedi toohello [portale di Azure classico](http://manage.windowsazure.com), fare clic su **Machine Learning** nella colonna sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="35af6-130">Sign in toohello [Azure classic portal](http://manage.windowsazure.com), click **Machine Learning** in hello left column.</span></span> <span data-ttu-id="35af6-131">Fare clic su area di lavoro hello che contiene il servizio Web hello in cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="35af6-131">Click hello workspace which contains hello Web service in which you are interested.</span></span>
   
    ![Passare tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. <span data-ttu-id="35af6-133">Fare clic su **Servizi Web**.</span><span class="sxs-lookup"><span data-stu-id="35af6-133">Click **Web Services**.</span></span>
   
    ![Passare a servizi tooWeb](./media/machine-learning-create-endpoint/figure-2.png)
3. <span data-ttu-id="35af6-135">Fare clic su servizio Web hello desiderati nell'elenco di hello toosee di endpoint disponibili.</span><span class="sxs-lookup"><span data-stu-id="35af6-135">Click hello Web service you're interested in toosee hello list of available endpoints.</span></span>
   
    ![Passare tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. <span data-ttu-id="35af6-137">Nella parte inferiore di hello della pagina hello, fare clic su **Aggiungi Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="35af6-137">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="35af6-138">Digitare un nome e descrizione, verificare che non sono presenti altri endpoint con hello stesso nome in questo servizio Web.</span><span class="sxs-lookup"><span data-stu-id="35af6-138">Type a name and description, ensure there are no other endpoints with hello same name in this Web service.</span></span> <span data-ttu-id="35af6-139">Lasciare il livello di limitazione hello con il valore predefinito a meno che non si hanno esigenze particolari.</span><span class="sxs-lookup"><span data-stu-id="35af6-139">Leave hello throttle level with its default value unless you have special requirements.</span></span> <span data-ttu-id="35af6-140">toolearn più sulla limitazione, vedere [gli endpoint dell'API scalabilità](machine-learning-scaling-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="35af6-140">toolearn more about throttling, see [Scaling API Endpoints](machine-learning-scaling-webservice.md).</span></span>
   
    ![Creare un endpoint](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a><span data-ttu-id="35af6-142">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="35af6-142">Next Steps</span></span>
<span data-ttu-id="35af6-143">[Come un servizio Web di Azure Machine Learning tooconsume](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="35af6-143">[How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

