---
title: Informazioni su come gestire i servizi Web di AzureML con Gestione API | Documentazione Microsoft
description: Guida che mostra come gestire i servizi Web di AzureML con Gestione API.
keywords: apprendimento automatico, gestione api
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 65eff3f4971f79886a840bb19bf76aaab48878de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="learn-how-to-manage-azureml-web-services-using-api-management"></a><span data-ttu-id="40860-104">Informazioni su come gestire i servizi Web di AzureML con Gestione API</span><span class="sxs-lookup"><span data-stu-id="40860-104">Learn how to manage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="40860-105">Overview</span><span class="sxs-lookup"><span data-stu-id="40860-105">Overview</span></span>
<span data-ttu-id="40860-106">Questa guida illustra le procedure per iniziare subito a usare Gestione API per gestire i servizi Web di AzureML.</span><span class="sxs-lookup"><span data-stu-id="40860-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="40860-107">Cos'è Gestione API di Azure?</span><span class="sxs-lookup"><span data-stu-id="40860-107">What is Azure API Management?</span></span>
<span data-ttu-id="40860-108">Gestione API di Azure è un servizio di Azure che consente di gestire gli endpoint dell'API REST definendo l'accesso utente, la limitazione all'utilizzo e il monitoraggio del dashboard.</span><span class="sxs-lookup"><span data-stu-id="40860-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="40860-109">Per informazioni dettagliate su Gestione API di Azure, fare clic [qui](https://azure.microsoft.com/services/api-management/) .</span><span class="sxs-lookup"><span data-stu-id="40860-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="40860-110">Per una guida introduttiva a Gestione API di Azure, fare clic [qui](../api-management/api-management-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="40860-110">Click [here](../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span></span> <span data-ttu-id="40860-111">L'altra guida, su cui è basata questa, tratta più argomenti, tra cui le configurazioni delle notifiche, il livello di prezzo, la gestione delle risposte, l'autenticazione utente, la creazione di prodotti, le sottoscrizioni per sviluppatori e il dashboarding dell'uso.</span><span class="sxs-lookup"><span data-stu-id="40860-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="40860-112">Informazioni su AzureML</span><span class="sxs-lookup"><span data-stu-id="40860-112">What is AzureML?</span></span>
<span data-ttu-id="40860-113">AzureML è un servizio di Azure basato su Machine Learning che consente di compilare, distribuire e condividere facilmente soluzioni di analisi avanzate.</span><span class="sxs-lookup"><span data-stu-id="40860-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="40860-114">Per informazioni dettagliate su AzureML, fare clic [qui](https://azure.microsoft.com/services/machine-learning/) .</span><span class="sxs-lookup"><span data-stu-id="40860-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="40860-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="40860-115">Prerequisites</span></span>
<span data-ttu-id="40860-116">Per completare questa guida, è necessario:</span><span class="sxs-lookup"><span data-stu-id="40860-116">To complete this guide, you need:</span></span>

* <span data-ttu-id="40860-117">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="40860-117">An Azure account.</span></span> <span data-ttu-id="40860-118">Se non si dispone di un account Azure, fare clic [qui](https://azure.microsoft.com/pricing/free-trial/) per informazioni dettagliate su come creare un account di prova gratuito.</span><span class="sxs-lookup"><span data-stu-id="40860-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="40860-119">Un account AzureML.</span><span class="sxs-lookup"><span data-stu-id="40860-119">An AzureML account.</span></span> <span data-ttu-id="40860-120">Se non si dispone di un account AzureML, fare clic [qui](https://studio.azureml.net/) per informazioni dettagliate su come creare un account di prova gratuito.</span><span class="sxs-lookup"><span data-stu-id="40860-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="40860-121">L'area di lavoro, il servizio e l'api_key per un esperimento di AzureML distribuito come servizio web.</span><span class="sxs-lookup"><span data-stu-id="40860-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="40860-122">Per informazioni dettagliate su come creare un esperimento di AzureML, fare clic [qui](machine-learning-create-experiment.md) .</span><span class="sxs-lookup"><span data-stu-id="40860-122">Click [here](machine-learning-create-experiment.md) for details on how to create an AzureML experiment.</span></span> <span data-ttu-id="40860-123">Per informazioni dettagliate su come distribuire un esperimento di AzureML come servizio Web, fare clic [qui](machine-learning-publish-a-machine-learning-web-service.md) .</span><span class="sxs-lookup"><span data-stu-id="40860-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="40860-124">In alternativa, l'Appendice A contiene le istruzioni per creare e testare un semplice esperimento di AzureML e distribuirlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="40860-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="40860-125">Creare un'istanza di Gestione API</span><span class="sxs-lookup"><span data-stu-id="40860-125">Create an API Management instance</span></span>
<span data-ttu-id="40860-126">Di seguito sono riportati i passaggi per gestire il servizio Web di AzureML con Gestione API.</span><span class="sxs-lookup"><span data-stu-id="40860-126">Below are the steps for using API Management to manage your AzureML web service.</span></span> <span data-ttu-id="40860-127">Creare innanzitutto un'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="40860-127">First create a service instance.</span></span> <span data-ttu-id="40860-128">Accedere al [portale classico](https://manage.windowsazure.com/) e fare clic su **Nuovo** > **Servizi app** > **Gestione API** > **Crea**.</span><span class="sxs-lookup"><span data-stu-id="40860-128">Log in to the [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="40860-130">Specificare un **URL**univoco.</span><span class="sxs-lookup"><span data-stu-id="40860-130">Specify a unique **URL**.</span></span> <span data-ttu-id="40860-131">Questa guida usa **demoazureml** : sarà necessario sceglierne uno diverso.</span><span class="sxs-lookup"><span data-stu-id="40860-131">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="40860-132">Scegliere **Sottoscrizione** e **Area** per l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="40860-132">Choose the desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="40860-133">Una volta effettuate le selezioni, fare clic sul pulsante Avanti.</span><span class="sxs-lookup"><span data-stu-id="40860-133">After making your selections, click the next button.</span></span>

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="40860-135">Specificare un valore per **Nome organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="40860-135">Specify a value for the **Organization Name**.</span></span> <span data-ttu-id="40860-136">Questa guida usa **demoazureml** : sarà necessario sceglierne uno diverso.</span><span class="sxs-lookup"><span data-stu-id="40860-136">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="40860-137">Immettere l'indirizzo di posta elettronica nel campo **Indirizzo di posta elettronica dell'amministratore** .</span><span class="sxs-lookup"><span data-stu-id="40860-137">Enter your email address in the **administrator e-mail** field.</span></span> <span data-ttu-id="40860-138">Questo indirizzo di posta elettronica viene usato per le notifiche inviate dal sistema Gestione API.</span><span class="sxs-lookup"><span data-stu-id="40860-138">This email address is used for notifications from the API Management system.</span></span>

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="40860-140">Selezionare la casella di controllo per creare l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="40860-140">Click the check box to create your service instance.</span></span> <span data-ttu-id="40860-141">*La creazione di un nuovo servizio richiede fino a trenta minuti*.</span><span class="sxs-lookup"><span data-stu-id="40860-141">*It takes up to thirty minutes for a new service to be created*.</span></span>

## <a name="create-the-api"></a><span data-ttu-id="40860-142">Creare l'API</span><span class="sxs-lookup"><span data-stu-id="40860-142">Create the API</span></span>
<span data-ttu-id="40860-143">Dopo aver creato l'istanza del servizio, l'operazione successiva consiste nel creare l'API.</span><span class="sxs-lookup"><span data-stu-id="40860-143">Once the service instance is created, the next step is to create the API.</span></span> <span data-ttu-id="40860-144">Un'API rappresenta un set di operazioni che possono essere richiamate da un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="40860-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="40860-145">Le operazioni API vengono trasmesse tramite proxy ai servizi Web esistenti.</span><span class="sxs-lookup"><span data-stu-id="40860-145">API operations are proxied to existing web services.</span></span> <span data-ttu-id="40860-146">Questa guida crea le API che usano un proxy per i servizi Web RRS e BES di AzureML esistenti.</span><span class="sxs-lookup"><span data-stu-id="40860-146">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="40860-147">Le API vengono create e configurate dal portale di pubblicazione delle API, accessibile dal portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="40860-147">APIs are created and configured from the API publisher portal, which is accessed through the Azure Classic Portal.</span></span> <span data-ttu-id="40860-148">Per raggiungere il portale di pubblicazione, selezionare l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="40860-148">To reach the publisher portal, select your service instance.</span></span>

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="40860-150">Fare clic su **Gestisci** nel portale di Azure classico per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="40860-150">Click **Manage** in the Azure Classic Portal for your API Management service.</span></span>

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="40860-152">Fare clic su **API** dal menu **Gestione API** sulla sinistra, quindi scegliere **Aggiungi API**.</span><span class="sxs-lookup"><span data-stu-id="40860-152">Click **APIs** from the **API Management** menu on the left, and then click **Add API**.</span></span>

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="40860-154">Digitare **AzureML Demo API** in **Nome API Web**.</span><span class="sxs-lookup"><span data-stu-id="40860-154">Type **AzureML Demo API** as the **Web API name**.</span></span> <span data-ttu-id="40860-155">Digitare **https://ussouthcentral.services.azureml.net** in **URL del servizio Web**.</span><span class="sxs-lookup"><span data-stu-id="40860-155">Type **https://ussouthcentral.services.azureml.net** as the **Web service URL**.</span></span> <span data-ttu-id="40860-156">Digitare **azureml-demo** in **Web API URL suffix** (Suffisso URL API Web).</span><span class="sxs-lookup"><span data-stu-id="40860-156">Type **azureml-demo** as the **Web API URL suffix**.</span></span> <span data-ttu-id="40860-157">Selezionare **HTTPS** come schema dell'**URL API Web**.</span><span class="sxs-lookup"><span data-stu-id="40860-157">Check **HTTPS** as the **Web API URL** scheme.</span></span> <span data-ttu-id="40860-158">Selezionare **Starter** (Avviatore) in **Prodotti**.</span><span class="sxs-lookup"><span data-stu-id="40860-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="40860-159">Al termine, fare clic su **Salva** per creare l'API.</span><span class="sxs-lookup"><span data-stu-id="40860-159">When finished, click **Save** to create the API.</span></span>

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-the-operations"></a><span data-ttu-id="40860-161">Aggiungere le operazioni</span><span class="sxs-lookup"><span data-stu-id="40860-161">Add the operations</span></span>
<span data-ttu-id="40860-162">Fare clic su **Aggiungi operazione** per aggiungere operazioni a questa API.</span><span class="sxs-lookup"><span data-stu-id="40860-162">Click **Add operation** to add operations to this API.</span></span>

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="40860-164">Verrà visualizzata la finestra **Nuova operazione** in cui la scheda **Firma** è selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="40860-164">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="40860-165">Aggiungere un'operazione RRS</span><span class="sxs-lookup"><span data-stu-id="40860-165">Add RRS Operation</span></span>
<span data-ttu-id="40860-166">Creare innanzitutto un'operazione per il servizio RRS di AzureML.</span><span class="sxs-lookup"><span data-stu-id="40860-166">First create an operation for the AzureML RRS service.</span></span> <span data-ttu-id="40860-167">Selezionare **POST** come **Verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="40860-167">Select **POST** as the **HTTP verb**.</span></span> <span data-ttu-id="40860-168">Digitare **/workspaces/{areadilavoro}/services/{servizio}/execute?api-version={versioneapi}&details={dettagli}** come **Modello di URL**.</span><span class="sxs-lookup"><span data-stu-id="40860-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as the **URL template**.</span></span> <span data-ttu-id="40860-169">Digitare **RRS Execute** in **Nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="40860-169">Type **RRS Execute** as the **Display name**.</span></span>

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="40860-171">Fare clic su **Risposte** > **AGGIUNGI** a sinistra e selezionare **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="40860-171">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="40860-172">Fare clic su **Salva** per salvare questa operazione.</span><span class="sxs-lookup"><span data-stu-id="40860-172">Click **Save** to save this operation.</span></span>

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="40860-174">Aggiungere operazioni BES</span><span class="sxs-lookup"><span data-stu-id="40860-174">Add BES Operations</span></span>
<span data-ttu-id="40860-175">Non sono incluse schermate per le operazioni di BES perché sono molto simili a quelle per l'aggiunta dell'operazione RRS.</span><span class="sxs-lookup"><span data-stu-id="40860-175">Screenshots are not included for the BES operations as they are very similar to those for adding the RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="40860-176">Inviare (ma non avviare) un processo di esecuzione in batch</span><span class="sxs-lookup"><span data-stu-id="40860-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="40860-177">Fare clic su **aggiungi operazione** per aggiungere l'operazione BES di AzureML all'API.</span><span class="sxs-lookup"><span data-stu-id="40860-177">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="40860-178">Selezionare **POST** in **Verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="40860-178">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="40860-179">Digitare **/workspaces/{areadilavoro}/services/{servizio}/jobs?api-version={versioneapi}** in **Modello URL**.</span><span class="sxs-lookup"><span data-stu-id="40860-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="40860-180">Digitare **BES Submit** in **Nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="40860-180">Type **BES Submit** for the **Display name**.</span></span> <span data-ttu-id="40860-181">Fare clic su **Risposte** > **AGGIUNGI** a sinistra e selezionare **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="40860-181">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="40860-182">Fare clic su **Salva** per salvare questa operazione.</span><span class="sxs-lookup"><span data-stu-id="40860-182">Click **Save** to save this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="40860-183">Avviare un processo di esecuzione in batch</span><span class="sxs-lookup"><span data-stu-id="40860-183">Start a Batch Execution job</span></span>
<span data-ttu-id="40860-184">Fare clic su **aggiungi operazione** per aggiungere l'operazione BES di AzureML all'API.</span><span class="sxs-lookup"><span data-stu-id="40860-184">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="40860-185">Selezionare **POST** in **Verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="40860-185">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="40860-186">Digitare **/workspaces/{areadilavoro}/services/{servizio}/jobs/{jobid}/start?api-version={versioneapi}** in **Modello URL**.</span><span class="sxs-lookup"><span data-stu-id="40860-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="40860-187">Digitare **BES Start** in **Nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="40860-187">Type **BES Start** for the **Display name**.</span></span> <span data-ttu-id="40860-188">Fare clic su **Risposte** > **AGGIUNGI** a sinistra e selezionare **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="40860-188">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="40860-189">Fare clic su **Salva** per salvare questa operazione.</span><span class="sxs-lookup"><span data-stu-id="40860-189">Click **Save** to save this operation.</span></span>

### <a name="get-the-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="40860-190">Ottenere lo stato o il risultato di un processo di esecuzione del Batch</span><span class="sxs-lookup"><span data-stu-id="40860-190">Get the status or result of a Batch Execution job</span></span>
<span data-ttu-id="40860-191">Fare clic su **aggiungi operazione** per aggiungere l'operazione BES di AzureML all'API.</span><span class="sxs-lookup"><span data-stu-id="40860-191">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="40860-192">Selezionare **GET** in **Verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="40860-192">Select **GET** for the **HTTP verb**.</span></span> <span data-ttu-id="40860-193">Digitare **/workspaces/{areadilavoro}/services/{servizio}/jobs/{jobid}?api-version={versioneapi}** in **Modello URL**.</span><span class="sxs-lookup"><span data-stu-id="40860-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="40860-194">Digitare **BES Status** in **Nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="40860-194">Type **BES Status** for the **Display name**.</span></span> <span data-ttu-id="40860-195">Fare clic su **Risposte** > **AGGIUNGI** a sinistra e selezionare **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="40860-195">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="40860-196">Fare clic su **Salva** per salvare questa operazione.</span><span class="sxs-lookup"><span data-stu-id="40860-196">Click **Save** to save this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="40860-197">Eliminare un processo di esecuzione in batch</span><span class="sxs-lookup"><span data-stu-id="40860-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="40860-198">Fare clic su **aggiungi operazione** per aggiungere l'operazione BES di AzureML all'API.</span><span class="sxs-lookup"><span data-stu-id="40860-198">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="40860-199">Selezionare **DELETE** in **Verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="40860-199">Select **DELETE** for the **HTTP verb**.</span></span> <span data-ttu-id="40860-200">Digitare **/workspaces/{areadilavoro}/services/{servizio}/jobs/{jobid}?api-version={versioneapi}** in **Modello URL**.</span><span class="sxs-lookup"><span data-stu-id="40860-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="40860-201">Digitare **BES Delete** in **Nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="40860-201">Type **BES Delete** for the **Display name**.</span></span> <span data-ttu-id="40860-202">Fare clic su **Risposte** > **AGGIUNGI** a sinistra e selezionare **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="40860-202">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="40860-203">Fare clic su **Salva** per salvare questa operazione.</span><span class="sxs-lookup"><span data-stu-id="40860-203">Click **Save** to save this operation.</span></span>

## <a name="call-an-operation-from-the-developer-portal"></a><span data-ttu-id="40860-204">Chiamare un'operazione dal portale per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="40860-204">Call an operation from the Developer Portal</span></span>
<span data-ttu-id="40860-205">È possibile chiamare le operazioni direttamente dal portale per sviluppatori, che consente di visualizzare e testare le operazioni di un'API in tutta comodità.</span><span class="sxs-lookup"><span data-stu-id="40860-205">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="40860-206">In questo passaggio della guida si chiamerà il metodo **RRS Execute** aggiunto all'**AzureML Demo API**.</span><span class="sxs-lookup"><span data-stu-id="40860-206">In this guide step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span></span> <span data-ttu-id="40860-207">Fare clic su **Portale per sviluppatori** nel menu in alto a destra del portale classico.</span><span class="sxs-lookup"><span data-stu-id="40860-207">Click **Developer portal** from the menu at the top right of the Classic Portal.</span></span>

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="40860-209">Fare clic su **API** nel menu superiore e quindi su **AzureML Demo API** per visualizzare le operazioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="40860-209">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="40860-211">Selezionare **RRS Execute** come operazione.</span><span class="sxs-lookup"><span data-stu-id="40860-211">Select **RRS Execute** for the operation.</span></span> <span data-ttu-id="40860-212">Fare clic su **Prova**.</span><span class="sxs-lookup"><span data-stu-id="40860-212">Click **Try It**.</span></span>

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="40860-214">Per i parametri della richiesta, digitare l'**area di lavoro**, il **servizio**, **2.0** per la **versione API** e **true** per i **dettagli**.</span><span class="sxs-lookup"><span data-stu-id="40860-214">For Request parameters, type your **workspace**,  **service**, **2.0** for the **apiversion**, and  **true** for the **details**.</span></span> <span data-ttu-id="40860-215">È possibile trovare l'**area di lavoro** e il **servizio** nel dashboard del servizio Web di AzureML (vedere **Testare il servizio Web** nell'Appendice A).</span><span class="sxs-lookup"><span data-stu-id="40860-215">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="40860-216">Per le intestazioni della richiesta, fare clic su **Aggiungi intestazione**, digitare **Content-Type** e **application/json**, quindi fare clic su **Aggiungi intestazione** e digitare **Authorization** e **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span><span class="sxs-lookup"><span data-stu-id="40860-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="40860-217">È possibile trovare la **chiave API** nel dashboard del servizio Web di AzureML (vedere **Testare il servizio Web** nell'Appendice A).</span><span class="sxs-lookup"><span data-stu-id="40860-217">You can find your **api key** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="40860-218">Digitare **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** come corpo della richiesta.</span><span class="sxs-lookup"><span data-stu-id="40860-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for the request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="40860-220">Fare clic su **Send**.</span><span class="sxs-lookup"><span data-stu-id="40860-220">Click **Send**.</span></span>

![Send](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="40860-222">Una volta richiamata un'operazione, nel portale per sviluppatori vengono visualizzati l'**URL richiesto** restituito dal servizio back-end, lo **Stato della risposta**, le **Intestazioni della risposta** e l'eventuale **Contenuto della risposta**.</span><span class="sxs-lookup"><span data-stu-id="40860-222">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="40860-224">Appendice A - Creazione e test di un semplice servizio Web di AzureML</span><span class="sxs-lookup"><span data-stu-id="40860-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-the-experiment"></a><span data-ttu-id="40860-225">Creazione di un esperimento</span><span class="sxs-lookup"><span data-stu-id="40860-225">Creating the experiment</span></span>
<span data-ttu-id="40860-226">Di seguito sono riportati i passaggi per creare un semplice esperimento di AzureML e distribuirlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="40860-226">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="40860-227">Il servizio Web accetta come input una colonna di testo arbitrario e restituisce un set di funzionalità rappresentate come valori Integer.</span><span class="sxs-lookup"><span data-stu-id="40860-227">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="40860-228">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="40860-228">For example:</span></span>

| <span data-ttu-id="40860-229">Text</span><span class="sxs-lookup"><span data-stu-id="40860-229">Text</span></span> | <span data-ttu-id="40860-230">Testo con hash</span><span class="sxs-lookup"><span data-stu-id="40860-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="40860-231">This is a good day</span><span class="sxs-lookup"><span data-stu-id="40860-231">This is a good day</span></span> |<span data-ttu-id="40860-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="40860-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="40860-233">Per prima cosa, usando il browser preferito, andare a [https://studio.azureml.net/](https://studio.azureml.net/) e immettere le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="40860-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span></span> <span data-ttu-id="40860-234">Quindi creare un nuovo esperimento vuoto.</span><span class="sxs-lookup"><span data-stu-id="40860-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="40860-236">Rinominarlo **SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="40860-236">Rename it to **SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="40860-237">Espandere **Saved Datasets** (Set di dati salvati) e trascinare **Book Reviews from Amazon** (Recensioni di libri da Amazon) sull'esperimento.</span><span class="sxs-lookup"><span data-stu-id="40860-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="40860-239">Espandere **Data Transformation** (Trasformazioni di dati) e **Manipulation** (Manipolazione), quindi trascinare **Select Columns in Dataset** (Seleziona colonne in set di dati) sull'esperimento.</span><span class="sxs-lookup"><span data-stu-id="40860-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="40860-240">Connettere **Book Reviews from Amazon** (Recensioni sul libro da Amazon) a **Select Columns in Dataset** (Seleziona colonne in set di dati).</span><span class="sxs-lookup"><span data-stu-id="40860-240">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="40860-242">Fare clic su **Select Columns in Dataset** (Seleziona colonne in set di dati), quindi fare clic su **Launch column selector** (Avvia selettore di colonna) e selezionare **Col2**.</span><span class="sxs-lookup"><span data-stu-id="40860-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="40860-243">Fare clic sul segno di spunta per applicare queste modifiche.</span><span class="sxs-lookup"><span data-stu-id="40860-243">Click the checkmark to apply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="40860-245">Espandere **Text Analytics** (Analisi testo) e trascinare **Feature Hashing** sull'esperimento.</span><span class="sxs-lookup"><span data-stu-id="40860-245">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span></span> <span data-ttu-id="40860-246">Connettere **Select Columns in Dataset** (Seleziona colonne in set di dati) a **Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="40860-246">Connect **Select Columns in Dataset** to **Feature Hashing**.</span></span>

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="40860-248">Digitare **3** in **Hashing bitsize**.</span><span class="sxs-lookup"><span data-stu-id="40860-248">Type **3** for the **Hashing bitsize**.</span></span> <span data-ttu-id="40860-249">Verranno create 8 (23) colonne.</span><span class="sxs-lookup"><span data-stu-id="40860-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="40860-251">A questo punto, è possibile fare clic su **Run** per testare l'esperimento.</span><span class="sxs-lookup"><span data-stu-id="40860-251">At this point, you may want to click **Run** to test the experiment.</span></span>

![Run](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="40860-253">Creare un servizio Web</span><span class="sxs-lookup"><span data-stu-id="40860-253">Create a web service</span></span>
<span data-ttu-id="40860-254">Ora creare un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="40860-254">Now create a web service.</span></span> <span data-ttu-id="40860-255">Espandere **Servizio Web** e trascinare **Input** sull'esperimento.</span><span class="sxs-lookup"><span data-stu-id="40860-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="40860-256">Connettere **Input** a **Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="40860-256">Connect **Input** to **Feature Hashing**.</span></span> <span data-ttu-id="40860-257">Trascinare anche **output** sull'esperimento.</span><span class="sxs-lookup"><span data-stu-id="40860-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="40860-258">Connettere **Output** a **Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="40860-258">Connect **Output** to **Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="40860-260">Fare cli su **Publish web service**.</span><span class="sxs-lookup"><span data-stu-id="40860-260">Click **Publish web service**.</span></span>

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="40860-262">Fare clic su **Yes** per pubblicare l'esperimento.</span><span class="sxs-lookup"><span data-stu-id="40860-262">Click **Yes** to publish the experiment.</span></span>

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-the-web-service"></a><span data-ttu-id="40860-264">Testare il servizio Web</span><span class="sxs-lookup"><span data-stu-id="40860-264">Test the web service</span></span>
<span data-ttu-id="40860-265">Un servizio Web di AzureML è costituito dagli endpoint RSS (servizio di richiesta/risposta) e BES (servizio di esecuzione batch).</span><span class="sxs-lookup"><span data-stu-id="40860-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="40860-266">RSS è per l'esecuzione sincrona.</span><span class="sxs-lookup"><span data-stu-id="40860-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="40860-267">BES è per l'esecuzione di processi asincrona.</span><span class="sxs-lookup"><span data-stu-id="40860-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="40860-268">Per testare il servizio Web con la seguente origine Python di esempio, potrebbe essere necessario scaricare e installare Azure SDK per Python (vedere: [Come installare Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="40860-268">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="40860-269">Per la seguente origine di esempio, saranno necessari anche l'**area di lavoro**, il **servizio** e la **chiave API** dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="40860-269">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span></span> <span data-ttu-id="40860-270">È possibile trovare l'area di lavoro e il servizio facendo clic su **Richiesta/risposta** o su **Esecuzione batch** per l'esperimento nel dashboard del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="40860-270">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span></span>

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="40860-272">È possibile trovare la **chiave API** facendo clic sull'esperimento nel dashboard del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="40860-272">You can find the **api_key** by clicking your experiment in the web service dashboard.</span></span>

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="40860-274">Testare l'endpoint RRS</span><span class="sxs-lookup"><span data-stu-id="40860-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="40860-275">Pulsante Test</span><span class="sxs-lookup"><span data-stu-id="40860-275">Test button</span></span>
<span data-ttu-id="40860-276">Un modo semplice per testare l'endpoint RRS consiste nel fare clic su **Test** nel dashboard del servizio.</span><span class="sxs-lookup"><span data-stu-id="40860-276">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="40860-278">Digitare **This is a good day** in **col2**.</span><span class="sxs-lookup"><span data-stu-id="40860-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="40860-279">Fare clic sul segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="40860-279">Click the checkmark.</span></span>

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="40860-281">Verrà visualizzato qualcosa di simile a quanto segue</span><span class="sxs-lookup"><span data-stu-id="40860-281">You will see something like</span></span>

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="40860-283">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="40860-283">Sample Code</span></span>
<span data-ttu-id="40860-284">È possibile testare RRS anche dal codice client.</span><span class="sxs-lookup"><span data-stu-id="40860-284">Another way to test your RRS is from your client code.</span></span> <span data-ttu-id="40860-285">Se si fa clic su **Richiesta/risposta** sul dashboard e si scorre fino in fondo, si vedrà il codice di esempio per C#, Python e R. Si vedrà anche la sintassi della richiesta RRS, incluso l'URI della richiesta, le intestazioni e il corpo.</span><span class="sxs-lookup"><span data-stu-id="40860-285">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span></span>

<span data-ttu-id="40860-286">Questa guida mostra un esempio di Python funzionante.</span><span class="sxs-lookup"><span data-stu-id="40860-286">This guide shows a working Python example.</span></span> <span data-ttu-id="40860-287">Sarà necessario modificarlo con l'**area di lavoro**, il **servizio** e la **chiave API** dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="40860-287">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span>

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("The request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="40860-288">Testare l'endpoint BES</span><span class="sxs-lookup"><span data-stu-id="40860-288">Test BES endpoint</span></span>
<span data-ttu-id="40860-289">Fare clic su **Esecuzione batch** sul dashboard e scorrere fino in fondo.</span><span class="sxs-lookup"><span data-stu-id="40860-289">Click **Batch execution** on the dashboard and scroll to the bottom.</span></span> <span data-ttu-id="40860-290">Si vedrà il codice di esempio per C#, Python e R. Si vedrà anche la sintassi delle richieste BES per inviare un processo, avviare un processo, ottenere lo stato o i risultati di un processo ed eliminare un processo.</span><span class="sxs-lookup"><span data-stu-id="40860-290">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span></span>

<span data-ttu-id="40860-291">Questa guida mostra un esempio di Python funzionante.</span><span class="sxs-lookup"><span data-stu-id="40860-291">This guide shows a working Python example.</span></span> <span data-ttu-id="40860-292">È necessario modificarlo con l'**area di lavoro**, il **servizio** e la **chiave API** dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="40860-292">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="40860-293">È anche necessario modificare il **nome account di archiviazione**, la **chiave dell'account di archiviazione** e il **nome del contenitore di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="40860-293">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="40860-294">Infine sarà necessario modificare il percorso del **file di input** e il percorso del **file di output**.</span><span class="sxs-lookup"><span data-stu-id="40860-294">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH THE API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH THE LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH THE LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("The request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading the result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written to the file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("The results for " + outputName + " are available at the following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "The results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading the input to blob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded the input to blob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting the job...")
    # submit the job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove the enclosing double-quotes
    print("Job ID: " + job_id)
    # start the job
    print("Starting the job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking the job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in the follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
