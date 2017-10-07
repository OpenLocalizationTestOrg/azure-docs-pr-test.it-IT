---
title: aaaLearn come toomanage Azure ml web services tramite Gestione API | Documenti Microsoft
description: Una Guida che illustra come toomanage Azure ml web services tramite Gestione API.
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
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a><span data-ttu-id="f4311-104">Informazioni su come toomanage Azure ml web services tramite Gestione API</span><span class="sxs-lookup"><span data-stu-id="f4311-104">Learn how toomanage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="f4311-105">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f4311-105">Overview</span></span>
<span data-ttu-id="f4311-106">Questa guida illustra come tooquickly informazioni introduttive sull'utilizzo di servizi web di Azure ml toomanage gestione API.</span><span class="sxs-lookup"><span data-stu-id="f4311-106">This guide shows you how tooquickly get started using API Management toomanage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="f4311-107">Cos'è Gestione API di Azure?</span><span class="sxs-lookup"><span data-stu-id="f4311-107">What is Azure API Management?</span></span>
<span data-ttu-id="f4311-108">Gestione API di Azure è un servizio di Azure che consente di gestire gli endpoint dell'API REST definendo l'accesso utente, la limitazione all'utilizzo e il monitoraggio del dashboard.</span><span class="sxs-lookup"><span data-stu-id="f4311-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="f4311-109">Per informazioni dettagliate su Gestione API di Azure, fare clic [qui](https://azure.microsoft.com/services/api-management/) .</span><span class="sxs-lookup"><span data-stu-id="f4311-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="f4311-110">Fare clic su [qui](../api-management/api-management-get-started.md) per una Guida per la modalità di avvio tooget con gestione API di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4311-110">Click [here](../api-management/api-management-get-started.md) for a guide on how tooget started with Azure API Management.</span></span> <span data-ttu-id="f4311-111">L'altra guida, su cui è basata questa, tratta più argomenti, tra cui le configurazioni delle notifiche, il livello di prezzo, la gestione delle risposte, l'autenticazione utente, la creazione di prodotti, le sottoscrizioni per sviluppatori e il dashboarding dell'uso.</span><span class="sxs-lookup"><span data-stu-id="f4311-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="f4311-112">Informazioni su AzureML</span><span class="sxs-lookup"><span data-stu-id="f4311-112">What is AzureML?</span></span>
<span data-ttu-id="f4311-113">Azure ml è un servizio di Azure per l'apprendimento automatico che consente la compilazione tooeasily, distribuire e condividere soluzioni analitica avanzate.</span><span class="sxs-lookup"><span data-stu-id="f4311-113">AzureML is an Azure service for machine learning that enables you tooeasily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="f4311-114">Per informazioni dettagliate su AzureML, fare clic [qui](https://azure.microsoft.com/services/machine-learning/) .</span><span class="sxs-lookup"><span data-stu-id="f4311-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4311-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f4311-115">Prerequisites</span></span>
<span data-ttu-id="f4311-116">toocomplete questa Guida, è necessario:</span><span class="sxs-lookup"><span data-stu-id="f4311-116">toocomplete this guide, you need:</span></span>

* <span data-ttu-id="f4311-117">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="f4311-117">An Azure account.</span></span> <span data-ttu-id="f4311-118">Se non si dispone di un account Azure, fare clic su [qui](https://azure.microsoft.com/pricing/free-trial/) per informazioni dettagliate su come toocreate un account di prova.</span><span class="sxs-lookup"><span data-stu-id="f4311-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="f4311-119">Un account AzureML.</span><span class="sxs-lookup"><span data-stu-id="f4311-119">An AzureML account.</span></span> <span data-ttu-id="f4311-120">Se non si dispone di un account di Azure ml, fare clic su [qui](https://studio.azureml.net/) per informazioni dettagliate su come toocreate un account di prova.</span><span class="sxs-lookup"><span data-stu-id="f4311-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="f4311-121">area di lavoro Hello e del servizio api_key per un esperimento di Azure ml distribuito come servizio web.</span><span class="sxs-lookup"><span data-stu-id="f4311-121">hello workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="f4311-122">Fare clic su [qui](machine-learning-create-experiment.md) per informazioni dettagliate sulla modalità di sperimentare toocreate un Azure ml.</span><span class="sxs-lookup"><span data-stu-id="f4311-122">Click [here](machine-learning-create-experiment.md) for details on how toocreate an AzureML experiment.</span></span> <span data-ttu-id="f4311-123">Fare clic su [qui](machine-learning-publish-a-machine-learning-web-service.md) per informazioni dettagliate su come toodeploy un Azure ml esperimento come servizio web.</span><span class="sxs-lookup"><span data-stu-id="f4311-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how toodeploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="f4311-124">In alternativa, nell'appendice contiene istruzioni di toocreate test un Azure ml semplice esperimento ed e distribuirla come servizio web.</span><span class="sxs-lookup"><span data-stu-id="f4311-124">Alternately, Appendix A has instructions for how toocreate and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="f4311-125">Creare un'istanza di Gestione API</span><span class="sxs-lookup"><span data-stu-id="f4311-125">Create an API Management instance</span></span>
<span data-ttu-id="f4311-126">Di seguito sono passaggi hello per l'utilizzo di gestione API toomanage il servizio web di Azure ml.</span><span class="sxs-lookup"><span data-stu-id="f4311-126">Below are hello steps for using API Management toomanage your AzureML web service.</span></span> <span data-ttu-id="f4311-127">Creare innanzitutto un'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="f4311-127">First create a service instance.</span></span> <span data-ttu-id="f4311-128">Accedi toohello [portale classico](https://manage.windowsazure.com/) e fare clic su **New** > **servizi App** > **gestione API**  >  **Creare**.</span><span class="sxs-lookup"><span data-stu-id="f4311-128">Log in toohello [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="f4311-130">Specificare un **URL**univoco.</span><span class="sxs-lookup"><span data-stu-id="f4311-130">Specify a unique **URL**.</span></span> <span data-ttu-id="f4311-131">Questa Guida usa **demoazureml** – toochoose sarà necessario un valore diverso.</span><span class="sxs-lookup"><span data-stu-id="f4311-131">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="f4311-132">Scegliere hello desiderato **sottoscrizione** e **area** per l'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="f4311-132">Choose hello desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="f4311-133">Dopo aver effettuato le selezioni, fare clic sul pulsante Avanti hello.</span><span class="sxs-lookup"><span data-stu-id="f4311-133">After making your selections, click hello next button.</span></span>

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="f4311-135">Specificare un valore per hello **nome organizzazione**.</span><span class="sxs-lookup"><span data-stu-id="f4311-135">Specify a value for hello **Organization Name**.</span></span> <span data-ttu-id="f4311-136">Questa Guida usa **demoazureml** – toochoose sarà necessario un valore diverso.</span><span class="sxs-lookup"><span data-stu-id="f4311-136">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="f4311-137">Immettere l'indirizzo di posta elettronica in hello **posta elettronica amministratore** campo.</span><span class="sxs-lookup"><span data-stu-id="f4311-137">Enter your email address in hello **administrator e-mail** field.</span></span> <span data-ttu-id="f4311-138">Questo indirizzo di posta elettronica viene utilizzato per notifiche da hello sistema gestione API.</span><span class="sxs-lookup"><span data-stu-id="f4311-138">This email address is used for notifications from hello API Management system.</span></span>

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="f4311-140">Fare clic su hello casella di controllo toocreate all'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="f4311-140">Click hello check box toocreate your service instance.</span></span> <span data-ttu-id="f4311-141">*Occupi toothirty minuti per un nuovo toobe servizio creato*.</span><span class="sxs-lookup"><span data-stu-id="f4311-141">*It takes up toothirty minutes for a new service toobe created*.</span></span>

## <a name="create-hello-api"></a><span data-ttu-id="f4311-142">Creare API hello</span><span class="sxs-lookup"><span data-stu-id="f4311-142">Create hello API</span></span>
<span data-ttu-id="f4311-143">Una volta creata l'istanza del servizio hello, hello sarà toocreate hello API.</span><span class="sxs-lookup"><span data-stu-id="f4311-143">Once hello service instance is created, hello next step is toocreate hello API.</span></span> <span data-ttu-id="f4311-144">Un'API rappresenta un set di operazioni che possono essere richiamate da un'applicazione client.</span><span class="sxs-lookup"><span data-stu-id="f4311-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="f4311-145">Le operazioni dell'API sono servizi web tooexisting elaborate.</span><span class="sxs-lookup"><span data-stu-id="f4311-145">API operations are proxied tooexisting web services.</span></span> <span data-ttu-id="f4311-146">Questa Guida consente di creare le API che toohello proxy AzureML RRS e BES servizi web esistenti.</span><span class="sxs-lookup"><span data-stu-id="f4311-146">This guide creates APIs that proxy toohello existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="f4311-147">API create e configurate dal portale di pubblicazione di hello API, è possibile accedervi tramite hello portale classico di Azure.</span><span class="sxs-lookup"><span data-stu-id="f4311-147">APIs are created and configured from hello API publisher portal, which is accessed through hello Azure Classic Portal.</span></span> <span data-ttu-id="f4311-148">tooreach hello selezionare portale, server di pubblicazione all'istanza del servizio.</span><span class="sxs-lookup"><span data-stu-id="f4311-148">tooreach hello publisher portal, select your service instance.</span></span>

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="f4311-150">Fare clic su **Gestisci** in hello portale classico di Azure per il servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="f4311-150">Click **Manage** in hello Azure Classic Portal for your API Management service.</span></span>

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="f4311-152">Fare clic su **API** da hello **gestione API** menu hello a sinistra e quindi fare clic su **aggiungere API**.</span><span class="sxs-lookup"><span data-stu-id="f4311-152">Click **APIs** from hello **API Management** menu on hello left, and then click **Add API**.</span></span>

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="f4311-154">Tipo **API di Azure ml Demo** come hello **nome API Web**.</span><span class="sxs-lookup"><span data-stu-id="f4311-154">Type **AzureML Demo API** as hello **Web API name**.</span></span> <span data-ttu-id="f4311-155">Tipo **https://ussouthcentral.services.azureml.net** come hello **URL servizio Web**.</span><span class="sxs-lookup"><span data-stu-id="f4311-155">Type **https://ussouthcentral.services.azureml.net** as hello **Web service URL**.</span></span> <span data-ttu-id="f4311-156">Tipo **demo di Azure ml** come hello **suffisso URL dell'API Web**.</span><span class="sxs-lookup"><span data-stu-id="f4311-156">Type **azureml-demo** as hello **Web API URL suffix**.</span></span> <span data-ttu-id="f4311-157">Controllare **HTTPS** come hello **l'URL dell'API Web** schema.</span><span class="sxs-lookup"><span data-stu-id="f4311-157">Check **HTTPS** as hello **Web API URL** scheme.</span></span> <span data-ttu-id="f4311-158">Selezionare **Starter** (Avviatore) in **Prodotti**.</span><span class="sxs-lookup"><span data-stu-id="f4311-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="f4311-159">Al termine, fare clic su **salvare** toocreate hello API.</span><span class="sxs-lookup"><span data-stu-id="f4311-159">When finished, click **Save** toocreate hello API.</span></span>

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a><span data-ttu-id="f4311-161">Aggiungere le operazioni di hello</span><span class="sxs-lookup"><span data-stu-id="f4311-161">Add hello operations</span></span>
<span data-ttu-id="f4311-162">Fare clic su **l'operazione di aggiunta** tooadd operazioni toothis API.</span><span class="sxs-lookup"><span data-stu-id="f4311-162">Click **Add operation** tooadd operations toothis API.</span></span>

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="f4311-164">Hello **nuova operazione** finestra verranno visualizzate e hello **firma** scheda verrà selezionata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="f4311-164">hello **New operation** window will be displayed and hello **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="f4311-165">Aggiungere un'operazione RRS</span><span class="sxs-lookup"><span data-stu-id="f4311-165">Add RRS Operation</span></span>
<span data-ttu-id="f4311-166">Creare innanzitutto un'operazione per il servizio AzureML RRS hello.</span><span class="sxs-lookup"><span data-stu-id="f4311-166">First create an operation for hello AzureML RRS service.</span></span> <span data-ttu-id="f4311-167">Selezionare **POST** come hello **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f4311-167">Select **POST** as hello **HTTP verb**.</span></span> <span data-ttu-id="f4311-168">Tipo **/workspaces/ {area di lavoro} / Services / {servizio} / execute? api-version = {apiversion} & dettagli = {dettagli}** come hello **modello di URL**.</span><span class="sxs-lookup"><span data-stu-id="f4311-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as hello **URL template**.</span></span> <span data-ttu-id="f4311-169">Tipo **RR eseguire** come hello **nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="f4311-169">Type **RRS Execute** as hello **Display name**.</span></span>

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="f4311-171">Fare clic su **risposte** > **aggiungere** su hello a sinistra e seleziona **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f4311-171">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="f4311-172">Fare clic su **salvare** toosave questa operazione.</span><span class="sxs-lookup"><span data-stu-id="f4311-172">Click **Save** toosave this operation.</span></span>

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="f4311-174">Aggiungere operazioni BES</span><span class="sxs-lookup"><span data-stu-id="f4311-174">Add BES Operations</span></span>
<span data-ttu-id="f4311-175">Schermate non sono incluse per hello operazioni BES come se fossero toothose molto simili per l'aggiunta di operazione RR hello.</span><span class="sxs-lookup"><span data-stu-id="f4311-175">Screenshots are not included for hello BES operations as they are very similar toothose for adding hello RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="f4311-176">Inviare (ma non avviare) un processo di esecuzione in batch</span><span class="sxs-lookup"><span data-stu-id="f4311-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="f4311-177">Fare clic su **l'operazione di aggiunta** tooadd hello Azure ml BES operazione toohello API.</span><span class="sxs-lookup"><span data-stu-id="f4311-177">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="f4311-178">Selezionare **POST** per hello **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f4311-178">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="f4311-179">Tipo **/workspaces/ {area di lavoro} / Services / {servizio} / processi? api-version = {apiversion}** per hello **modello di URL**.</span><span class="sxs-lookup"><span data-stu-id="f4311-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="f4311-180">Tipo **inviare BES** per hello **nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="f4311-180">Type **BES Submit** for hello **Display name**.</span></span> <span data-ttu-id="f4311-181">Fare clic su **risposte** > **aggiungere** su hello a sinistra e seleziona **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f4311-181">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="f4311-182">Fare clic su **salvare** toosave questa operazione.</span><span class="sxs-lookup"><span data-stu-id="f4311-182">Click **Save** toosave this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="f4311-183">Avviare un processo di esecuzione in batch</span><span class="sxs-lookup"><span data-stu-id="f4311-183">Start a Batch Execution job</span></span>
<span data-ttu-id="f4311-184">Fare clic su **l'operazione di aggiunta** tooadd hello Azure ml BES operazione toohello API.</span><span class="sxs-lookup"><span data-stu-id="f4311-184">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="f4311-185">Selezionare **POST** per hello **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f4311-185">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="f4311-186">Tipo **/workspaces/ {area di lavoro} / Services / {servizio} /jobs/ {jobid} / avvia? api-version = {apiversion}** per hello **modello di URL**.</span><span class="sxs-lookup"><span data-stu-id="f4311-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="f4311-187">Tipo **avviare BES** per hello **nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="f4311-187">Type **BES Start** for hello **Display name**.</span></span> <span data-ttu-id="f4311-188">Fare clic su **risposte** > **aggiungere** su hello a sinistra e seleziona **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f4311-188">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="f4311-189">Fare clic su **salvare** toosave questa operazione.</span><span class="sxs-lookup"><span data-stu-id="f4311-189">Click **Save** toosave this operation.</span></span>

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="f4311-190">Ottenere lo stato di hello o il risultato di un processo di esecuzione Batch</span><span class="sxs-lookup"><span data-stu-id="f4311-190">Get hello status or result of a Batch Execution job</span></span>
<span data-ttu-id="f4311-191">Fare clic su **l'operazione di aggiunta** tooadd hello Azure ml BES operazione toohello API.</span><span class="sxs-lookup"><span data-stu-id="f4311-191">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="f4311-192">Selezionare **ottenere** per hello **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f4311-192">Select **GET** for hello **HTTP verb**.</span></span> <span data-ttu-id="f4311-193">Tipo **/workspaces/ {area di lavoro} / Services / {servizio} /jobs/ {jobid}? api-version = {apiversion}** per hello **modello di URL**.</span><span class="sxs-lookup"><span data-stu-id="f4311-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="f4311-194">Tipo **stato BES** per hello **nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="f4311-194">Type **BES Status** for hello **Display name**.</span></span> <span data-ttu-id="f4311-195">Fare clic su **risposte** > **aggiungere** su hello a sinistra e seleziona **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f4311-195">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="f4311-196">Fare clic su **salvare** toosave questa operazione.</span><span class="sxs-lookup"><span data-stu-id="f4311-196">Click **Save** toosave this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="f4311-197">Eliminare un processo di esecuzione in batch</span><span class="sxs-lookup"><span data-stu-id="f4311-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="f4311-198">Fare clic su **l'operazione di aggiunta** tooadd hello Azure ml BES operazione toohello API.</span><span class="sxs-lookup"><span data-stu-id="f4311-198">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="f4311-199">Selezionare **eliminare** per hello **verbo HTTP**.</span><span class="sxs-lookup"><span data-stu-id="f4311-199">Select **DELETE** for hello **HTTP verb**.</span></span> <span data-ttu-id="f4311-200">Tipo **/workspaces/ {area di lavoro} / Services / {servizio} /jobs/ {jobid}? api-version = {apiversion}** per hello **modello di URL**.</span><span class="sxs-lookup"><span data-stu-id="f4311-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="f4311-201">Tipo **eliminare BES** per hello **nome visualizzato**.</span><span class="sxs-lookup"><span data-stu-id="f4311-201">Type **BES Delete** for hello **Display name**.</span></span> <span data-ttu-id="f4311-202">Fare clic su **risposte** > **aggiungere** su hello a sinistra e seleziona **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f4311-202">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="f4311-203">Fare clic su **salvare** toosave questa operazione.</span><span class="sxs-lookup"><span data-stu-id="f4311-203">Click **Save** toosave this operation.</span></span>

## <a name="call-an-operation-from-hello-developer-portal"></a><span data-ttu-id="f4311-204">Chiamare un'operazione dal portale per sviluppatori hello</span><span class="sxs-lookup"><span data-stu-id="f4311-204">Call an operation from hello Developer Portal</span></span>
<span data-ttu-id="f4311-205">Operazioni possono essere chiamate direttamente dal portale per sviluppatori di hello, che fornisce un modo pratico di tooview e testare il funzionamento di hello di un'API.</span><span class="sxs-lookup"><span data-stu-id="f4311-205">Operations can be called directly from hello Developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="f4311-206">In questo passaggio Guida si chiamerà hello **RR eseguire** metodo che è stato aggiunto toohello **API di Azure ml Demo**.</span><span class="sxs-lookup"><span data-stu-id="f4311-206">In this guide step you will call hello **RRS Execute** method that was added toohello **AzureML Demo API**.</span></span> <span data-ttu-id="f4311-207">Fare clic su **portale per sviluppatori** dal menu hello hello in alto a destra di hello portale classico.</span><span class="sxs-lookup"><span data-stu-id="f4311-207">Click **Developer portal** from hello menu at hello top right of hello Classic Portal.</span></span>

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="f4311-209">Fare clic su **API** dal menu superiore hello e quindi fare clic su **API di Azure ml Demo** operazioni hello toosee disponibili.</span><span class="sxs-lookup"><span data-stu-id="f4311-209">Click **APIs** from hello top menu, and then click **AzureML Demo API** toosee hello operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="f4311-211">Selezionare **RR eseguire** per l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="f4311-211">Select **RRS Execute** for hello operation.</span></span> <span data-ttu-id="f4311-212">Fare clic su **Prova**.</span><span class="sxs-lookup"><span data-stu-id="f4311-212">Click **Try It**.</span></span>

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="f4311-214">Per i parametri di richiesta, digitare il **dell'area di lavoro**, **servizio**, **2.0** per hello **apiversion**, e **true**per hello **dettagli**.</span><span class="sxs-lookup"><span data-stu-id="f4311-214">For Request parameters, type your **workspace**,  **service**, **2.0** for hello **apiversion**, and  **true** for hello **details**.</span></span> <span data-ttu-id="f4311-215">È possibile trovare il **dell'area di lavoro** e **servizio** nel dashboard del servizio web di Azure ml hello (vedere **Test servizio web hello** nell'appendice).</span><span class="sxs-lookup"><span data-stu-id="f4311-215">You can find your **workspace** and **service** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="f4311-216">Per le intestazioni della richiesta, fare clic su **Aggiungi intestazione**, digitare **Content-Type** e **application/json**, quindi fare clic su **Aggiungi intestazione** e digitare **Authorization** e **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span><span class="sxs-lookup"><span data-stu-id="f4311-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="f4311-217">È possibile trovare il **chiave api** nel dashboard del servizio web di Azure ml hello (vedere **Test servizio web hello** nell'appendice).</span><span class="sxs-lookup"><span data-stu-id="f4311-217">You can find your **api key** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="f4311-218">Tipo **{"Input": {"input1": {"ColumnNames": "Valori" ["Col2"]: [["questo è un buon giorno"]]}}, "Globalparameters della": {}}** per il corpo della richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="f4311-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for hello request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="f4311-220">Fare clic su **Send**.</span><span class="sxs-lookup"><span data-stu-id="f4311-220">Click **Send**.</span></span>

![Send](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="f4311-222">Dopo un'operazione viene richiamata, il portale per sviluppatori di hello Visualizza hello **URL richiesto** dal servizio back-end hello, hello **stato della risposta**, hello **le intestazioni di risposta**, e qualsiasi **contenuto della risposta**.</span><span class="sxs-lookup"><span data-stu-id="f4311-222">After an operation is invoked, hello developer portal displays hello **Requested URL** from hello back-end service, hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="f4311-224">Appendice A - Creazione e test di un semplice servizio Web di AzureML</span><span class="sxs-lookup"><span data-stu-id="f4311-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-hello-experiment"></a><span data-ttu-id="f4311-225">Creazione di sperimentazione hello</span><span class="sxs-lookup"><span data-stu-id="f4311-225">Creating hello experiment</span></span>
<span data-ttu-id="f4311-226">Di seguito sono passaggi hello per la creazione di un semplice esperimento di Azure ml e distribuirla come servizio web.</span><span class="sxs-lookup"><span data-stu-id="f4311-226">Below are hello steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="f4311-227">Hello web servizio accetta come input una colonna di testo arbitrario e restituisce un set di funzionalità rappresentati come numeri interi.</span><span class="sxs-lookup"><span data-stu-id="f4311-227">hello web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="f4311-228">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f4311-228">For example:</span></span>

| <span data-ttu-id="f4311-229">Text</span><span class="sxs-lookup"><span data-stu-id="f4311-229">Text</span></span> | <span data-ttu-id="f4311-230">Testo con hash</span><span class="sxs-lookup"><span data-stu-id="f4311-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="f4311-231">This is a good day</span><span class="sxs-lookup"><span data-stu-id="f4311-231">This is a good day</span></span> |<span data-ttu-id="f4311-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="f4311-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="f4311-233">In primo luogo, usando un browser di propria scelta, passare a: [https://studio.azureml.net/](https://studio.azureml.net/) e immettere le credenziali toolog in.</span><span class="sxs-lookup"><span data-stu-id="f4311-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials toolog in.</span></span> <span data-ttu-id="f4311-234">Quindi creare un nuovo esperimento vuoto.</span><span class="sxs-lookup"><span data-stu-id="f4311-234">Next, create a new blank experiment.</span></span>

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="f4311-236">Rinominarlo troppo**SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="f4311-236">Rename it too**SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="f4311-237">Espandere **Saved Datasets** (Set di dati salvati) e trascinare **Book Reviews from Amazon** (Recensioni di libri da Amazon) sull'esperimento.</span><span class="sxs-lookup"><span data-stu-id="f4311-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="f4311-239">Espandere **Data Transformation** (Trasformazioni di dati) e **Manipulation** (Manipolazione), quindi trascinare **Select Columns in Dataset** (Seleziona colonne in set di dati) sull'esperimento.</span><span class="sxs-lookup"><span data-stu-id="f4311-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="f4311-240">Connettersi **recensioni da Amazon** troppo**selezionare le colonne nel set di dati**.</span><span class="sxs-lookup"><span data-stu-id="f4311-240">Connect **Book Reviews from Amazon** too**Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="f4311-242">Fare clic su **Select Columns in Dataset** (Seleziona colonne in set di dati), quindi fare clic su **Launch column selector** (Avvia selettore di colonna) e selezionare **Col2**.</span><span class="sxs-lookup"><span data-stu-id="f4311-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="f4311-243">Fare clic su hello segno di spunta tooapply queste modifiche.</span><span class="sxs-lookup"><span data-stu-id="f4311-243">Click hello checkmark tooapply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="f4311-245">Espandere **testo Analitica** e trascinare **Feature Hashing** nella sperimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="f4311-245">Expand **Text Analytics** and drag **Feature Hashing** onto hello experiment.</span></span> <span data-ttu-id="f4311-246">Connettersi **selezionare le colonne nel set di dati** troppo**Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="f4311-246">Connect **Select Columns in Dataset** too**Feature Hashing**.</span></span>

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="f4311-248">Tipo **3** per hello **Hashing bitsize**.</span><span class="sxs-lookup"><span data-stu-id="f4311-248">Type **3** for hello **Hashing bitsize**.</span></span> <span data-ttu-id="f4311-249">Verranno create 8 (23) colonne.</span><span class="sxs-lookup"><span data-stu-id="f4311-249">This will create 8 (23) columns.</span></span>

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="f4311-251">A questo punto, è opportuno tooclick **eseguire** esperimento hello tootest.</span><span class="sxs-lookup"><span data-stu-id="f4311-251">At this point, you may want tooclick **Run** tootest hello experiment.</span></span>

![Run](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="f4311-253">Creare un servizio Web</span><span class="sxs-lookup"><span data-stu-id="f4311-253">Create a web service</span></span>
<span data-ttu-id="f4311-254">Ora creare un servizio Web.</span><span class="sxs-lookup"><span data-stu-id="f4311-254">Now create a web service.</span></span> <span data-ttu-id="f4311-255">Espandere **Servizio Web** e trascinare **Input** sull'esperimento.</span><span class="sxs-lookup"><span data-stu-id="f4311-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="f4311-256">Connettersi **Input** troppo**Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="f4311-256">Connect **Input** too**Feature Hashing**.</span></span> <span data-ttu-id="f4311-257">Trascinare anche **output** sull'esperimento.</span><span class="sxs-lookup"><span data-stu-id="f4311-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="f4311-258">Connettersi **Output** troppo**Feature Hashing**.</span><span class="sxs-lookup"><span data-stu-id="f4311-258">Connect **Output** too**Feature Hashing**.</span></span>

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="f4311-260">Fare cli su **Publish web service**.</span><span class="sxs-lookup"><span data-stu-id="f4311-260">Click **Publish web service**.</span></span>

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="f4311-262">Fare clic su **Sì** esperimento hello toopublish.</span><span class="sxs-lookup"><span data-stu-id="f4311-262">Click **Yes** toopublish hello experiment.</span></span>

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a><span data-ttu-id="f4311-264">Servizio web hello di test</span><span class="sxs-lookup"><span data-stu-id="f4311-264">Test hello web service</span></span>
<span data-ttu-id="f4311-265">Un servizio Web di AzureML è costituito dagli endpoint RSS (servizio di richiesta/risposta) e BES (servizio di esecuzione batch).</span><span class="sxs-lookup"><span data-stu-id="f4311-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="f4311-266">RSS è per l'esecuzione sincrona.</span><span class="sxs-lookup"><span data-stu-id="f4311-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="f4311-267">BES è per l'esecuzione di processi asincrona.</span><span class="sxs-lookup"><span data-stu-id="f4311-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="f4311-268">tootest del servizio web con origine Python hello esempio riportato di seguito, potrebbe essere necessario toodownload e hello installare Azure SDK per Python (vedere: [come tooinstall Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="f4311-268">tootest your web service with hello sample Python source below, you may need toodownload and install hello Azure SDK for Python (see: [How tooinstall Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="f4311-269">È inoltre necessario hello **dell'area di lavoro**, **servizio**, e **api_key** dell'esperimento per l'origine di esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="f4311-269">You will also need hello **workspace**, **service**, and **api_key** of your experiment for hello sample source below.</span></span> <span data-ttu-id="f4311-270">È possibile trovare l'area di lavoro hello e il servizio facendo clic su **richiesta/risposta** o **esecuzione Batch** per l'esperimento nel dashboard del servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="f4311-270">You can find hello workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in hello web service dashboard.</span></span>

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="f4311-272">È possibile trovare hello **api_key** facendo esperimento nel dashboard del servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="f4311-272">You can find hello **api_key** by clicking your experiment in hello web service dashboard.</span></span>

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="f4311-274">Testare l'endpoint RRS</span><span class="sxs-lookup"><span data-stu-id="f4311-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="f4311-275">Pulsante Test</span><span class="sxs-lookup"><span data-stu-id="f4311-275">Test button</span></span>
<span data-ttu-id="f4311-276">Un endpoint di record di risorse facilmente tootest hello è tooclick **Test** nel dashboard del servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="f4311-276">An easy way tootest hello RRS endpoint is tooclick **Test** on hello web service dashboard.</span></span>

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="f4311-278">Digitare **This is a good day** in **col2**.</span><span class="sxs-lookup"><span data-stu-id="f4311-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="f4311-279">Fare clic su hello segno di spunta.</span><span class="sxs-lookup"><span data-stu-id="f4311-279">Click hello checkmark.</span></span>

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="f4311-281">Verrà visualizzato qualcosa di simile a quanto segue</span><span class="sxs-lookup"><span data-stu-id="f4311-281">You will see something like</span></span>

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="f4311-283">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="f4311-283">Sample Code</span></span>
<span data-ttu-id="f4311-284">Un altro modo tootest i record di risorse è dal codice client.</span><span class="sxs-lookup"><span data-stu-id="f4311-284">Another way tootest your RRS is from your client code.</span></span> <span data-ttu-id="f4311-285">Se si fa clic **richiesta/risposta** hello dashboard e scorrere toohello lato inferiore, verrà visualizzato il codice di esempio per c#, Python e R. Si verifica anche la sintassi di hello di richieste di record di risorse hello, inclusi hello richiesta URI, intestazioni e corpo.</span><span class="sxs-lookup"><span data-stu-id="f4311-285">If you click **Request/response** on hello dashboard and scroll toohello bottom, you will see sample code for C#, Python, and R. You will also see hello syntax of hello RRS request, including hello request URI, headers, and body.</span></span>

<span data-ttu-id="f4311-286">Questa guida mostra un esempio di Python funzionante.</span><span class="sxs-lookup"><span data-stu-id="f4311-286">This guide shows a working Python example.</span></span> <span data-ttu-id="f4311-287">Sarà necessario toomodify con hello **dell'area di lavoro**, **servizio**, e **api_key** dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="f4311-287">You will need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span>

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
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="f4311-288">Testare l'endpoint BES</span><span class="sxs-lookup"><span data-stu-id="f4311-288">Test BES endpoint</span></span>
<span data-ttu-id="f4311-289">Fare clic su **esecuzione Batch** nella parte inferiore di toohello dashboard e scorrere hello.</span><span class="sxs-lookup"><span data-stu-id="f4311-289">Click **Batch execution** on hello dashboard and scroll toohello bottom.</span></span> <span data-ttu-id="f4311-290">Verrà visualizzato il codice di esempio per c#, Python e R. Si verifica anche la sintassi di hello di hello BES richieste toosubmit un processo, avviare un processo, ottenere lo stato di hello o risultati di un processo ed eliminare un processo.</span><span class="sxs-lookup"><span data-stu-id="f4311-290">You will see sample code for C#, Python, and R. You will also see hello syntax of hello BES requests toosubmit a job, start a job, get hello status or results of a job, and delete a job.</span></span>

<span data-ttu-id="f4311-291">Questa guida mostra un esempio di Python funzionante.</span><span class="sxs-lookup"><span data-stu-id="f4311-291">This guide shows a working Python example.</span></span> <span data-ttu-id="f4311-292">È necessario toomodify con hello **dell'area di lavoro**, **servizio**, e **api_key** dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="f4311-292">You need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="f4311-293">Inoltre, è necessario hello toomodify **nome account di archiviazione**, **chiave account di archiviazione**, e **nome del contenitore di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="f4311-293">Additionally, you need toomodify hello **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="f4311-294">Infine, sarà necessario percorso hello toomodify di hello **file di input** e il percorso di hello di hello **file di output**.</span><span class="sxs-lookup"><span data-stu-id="f4311-294">Lastly, you will need toomodify hello location of hello **input file** and hello location of hello **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
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
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
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
